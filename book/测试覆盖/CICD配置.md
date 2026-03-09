# CI/CD 配置（GitHub Actions）

> 使用 GitHub Actions 实现 MCP 项目的自动化测试和部署

---

## CI/CD 流程概览

```
┌─────────────────────────────────────────────────────────────────┐
│                    MCP 项目 CI/CD 流程                           │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  ┌─────────┐    ┌─────────┐    ┌─────────┐    ┌─────────┐    │
│  │  Push   │───►│  Build  │───►│  Test   │───►│ Deploy │    │
│  │         │    │         │    │         │    │         │    │
│  └─────────┘    └─────────┘    └─────────┘    └─────────┘    │
│                    │               │               │           │
│                    ▼               ▼               ▼           │
│              ┌─────────┐    ┌─────────┐    ┌─────────┐        │
│              │Lint/    │    │Unit/    │    │Publish  │        │
│              │Format   │    │Integration│   │Package  │        │
│              └─────────┘    └─────────┘    └─────────┘        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 基础 CI 配置

```yaml
# .github/workflows/ci.yml
name: CI

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install -e ".[dev]"
          pip install pytest pytest-cov

      - name: Lint
        run: |
          pip install ruff
          ruff check src/

      - name: Format check
        run: |
          pip install black
          black --check src/

      - name: Type check
        run: |
          pip install mypy
          mypy src/

      - name: Run tests
        run: |
          pytest tests/ \
            --cov=src \
            --cov-report=xml \
            --cov-report=term-missing

      - name: Upload coverage
        uses: codecov/codecov-action@v4
        with:
          file: ./coverage.xml
```

---

## 多版本测试矩阵

```yaml
# .github/workflows/ci-matrix.yml
name: CI Matrix

on: [push, pull_request]

jobs:
  test:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: ['3.10', '3.11', '3.12']
        os: [ubuntu-latest, macos-latest, windows-latest]

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v5
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install dependencies
        run: |
          pip install -e ".[dev]"

      - name: Run tests
        run: |
          pytest tests/ -v
```

---

## 集成测试 CI

```yaml
# .github/workflows/ci-integration.yml
name: Integration Tests

on:
  push:
    branches: [main]
  schedule:
    - cron: '0 2 * * *'  # 每天凌晨运行

jobs:
  integration-test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:15
        env:
          POSTGRES_PASSWORD: test
          POSTGRES_DB: test_db
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

      redis:
        image: redis:7
        ports:
          - 6379:6379

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install -e ".[dev]"

      - name: Run integration tests
        run: |
          pytest tests/integration/ -v
        env:
          DATABASE_URL: postgresql://postgres:test@localhost:5432/test_db
          REDIS_URL: redis://localhost:6379
```

---

## CD 部署配置

```yaml
# .github/workflows/cd.yml
name: CD

on:
  push:
    tags:
      - 'v*'

jobs:
  build-and-publish:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: |
          pip install build

      - name: Build package
        run: |
          python -m build

      - name: Publish to PyPI
        uses: pypa/gh-action-pypi-publish@release/v1
        with:
          user: __token__
          password: ${{ secrets.PYPI_API_TOKEN }}

      - name: Create GitHub Release
        uses: actions/create-release@v1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          tag_name: ${{ github.ref }}
          release_name: Release ${{ github.ref }}
          draft: false
          prerelease: false
```

---

## MCP 服务器发布流程

```yaml
# .github/workflows/release-mcp-server.yml
name: Release MCP Server

on:
  release:
    types: [published]

jobs:
  release:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - name: Set up Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          registry-url: 'https://registry.npmjs.org'

      - name: Install dependencies
        run: |
          npm ci

      - name: Run tests
        run: |
          npm test

      - name: Build
        run: |
          npm run build

      - name: Publish to npm
        run: |
          npm publish --access public
        env:
          NODE_AUTH_TOKEN: ${{ secrets.NPM_TOKEN }}
```

---

## 本地开发工作流

```yaml
# .github/workflows/dev-workflow.yml
name: Dev Workflow

on:
  issue_comment:
    types: [created]

jobs:
  dev-test:
    if: contains(github.event.comment.body, '/test')
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4
        with:
          ref: ${{ github.event.issue.head_ref }}

      - name: Run development tests
        run: |
          pip install -e ".[dev]"
          pytest tests/ -v --tb=short

      - name: Comment results
        uses: actions/github-script@v7
        with:
          script: |
            github.rest.issues.createComment({
              issue_number: context.issue.number,
              owner: context.repo.owner,
              repo: context.repo.repo,
              body: '✅ Development tests passed!'
            })
```

---

## 测试覆盖率徽章

```markdown
<!-- README.md -->
[![Coverage](https://codecov.io/gh/your-org/your-repo/branch/main/graph/badge.svg)](https://codecov.io/gh/your-org/your-repo)
```

---

## 本章小结

1. **CI 基础**——代码检查、格式化、类型检查、单元测试
2. **测试矩阵**——多版本 Python 和多平台测试
3. **集成测试**——使用 Docker 服务进行测试
4. **CD 部署**——自动发布到 PyPI/npm
5. **工作流示例**——完整的 GitHub Actions 配置

---

## 相关资源

- [GitHub Actions 文档](https://docs.github.com/en/actions)
- [PyPI 发布 Action](https://github.com/pypa/gh-action-pypi-publish)
- [Codecov 集成](https://github.com/codecov/codecov-action)

---

*版本：v3.0*
