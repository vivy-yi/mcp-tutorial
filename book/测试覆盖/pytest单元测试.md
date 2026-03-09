# pytest 单元测试模板

> 为 MCP 服务器编写全面的单元测试

---

## 测试框架选择

```
┌─────────────────────────────────────────────────────────────────┐
│                    MCP 常用测试框架                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  Python:                                                        │
│  ├── pytest          - 主流测试框架，功能强大                   │
│  ├── pytest-asyncio  - 异步测试支持                            │
│  └── pytest-mock     - Mock 对象支持                            │
│                                                                 │
│  TypeScript:                                                     │
│  ├── Jest            - Facebook 出品，功能全面                 │
│  ├── Vitest          - Vite 原生，快速                          │
│  └── Mocha           - 传统可靠                                 │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 项目结构

```
mcp-project/
├── src/
│   └── server.py
├── tests/
│   ├── unit/
│   │   ├── __init__.py
│   │   └── test_tools.py
│   ├── integration/
│   │   ├── __init__.py
│   │   └── test_server.py
│   └── conftest.py
├── pyproject.toml
└── pytest.ini
```

---

## pytest 配置

### pyproject.toml

```toml
[build-system]
requires = ["setuptools>=61.0"]
build-backend = "setuptools.build_meta"

[project]
name = "my-mcp-server"
version = "0.1.0"
requires-python = ">=3.10"

[tool.pytest.ini_options]
testpaths = ["tests"]
python_files = ["test_*.py"]
python_classes = ["Test*"]
python_functions = ["test_*"]
asyncio_mode = "auto"
addopts = "-v --tb=short"
```

### conftest.py (共享 fixtures)

```python
import pytest
from fastmcp import FastMCP


@pytest.fixture
def app():
    """创建测试用的 MCP 应用"""
    return FastMCP("Test Server")


@pytest.fixture
def mock_github_response():
    """模拟 GitHub API 响应"""
    return {
        "id": 123,
        "name": "test-repo",
        "full_name": "testuser/test-repo",
        "private": False,
        "html_url": "https://github.com/testuser/test-repo"
    }
```

---

## 工具测试示例

```python
# tests/unit/test_tools.py
import pytest
from fastmcp import FastMCP

# 创建测试应用
app = FastMCP("Test Server")


@app.tool()
def add(a: int, b: int) -> int:
    """计算两个数的和"""
    return a + b


@app.tool()
def greet(name: str, greeting: str = "Hello") -> str:
    """生成问候语"""
    return f"{greeting}, {name}!"


class TestAddTool:
    """测试 add 工具"""

    def test_add_positive_numbers(self):
        """测试正数相加"""
        result = add(a=5, b=3)
        assert result == 8

    def test_add_negative_numbers(self):
        """测试负数相加"""
        result = add(a=-5, b=-3)
        assert result == -8

    def test_add_mixed_numbers(self):
        """测试正负数混合"""
        result = add(a=5, b=-3)
        assert result == 2

    def test_add_zero(self):
        """测试与零相加"""
        result = add(a=0, b=5)
        assert result == 5


class TestGreetTool:
    """测试 greet 工具"""

    def test_greet_default(self):
        """测试默认问候"""
        result = greet(name="World")
        assert result == "Hello, World!"

    def test_greet_custom_greeting(self):
        """测试自定义问候"""
        result = greet(name="Alice", greeting="Hi")
        assert result == "Hi, Alice!"

    def test_greet_empty_name(self):
        """测试空名字"""
        result = greet(name="")
        assert result == "Hello, !"


class TestToolDefinitions:
    """测试工具定义"""

    def test_add_tool_schema(self):
        """测试工具的 JSON Schema"""
        tools = app._tool_manager.list_tools()
        add_tool = next(t for t in tools if t.name == "add")

        assert add_tool.inputSchema["type"] == "object"
        assert "a" in add_tool.inputSchema["properties"]
        assert "b" in add_tool.inputSchema["properties"]

    def test_greet_tool_schema(self):
        """测试带可选参数的 schema"""
        tools = app._tool_manager.list_tools()
        greet_tool = next(t for t in tools if t.name == "greet")

        props = greet_tool.inputSchema["properties"]
        assert "name" in props
        assert "greeting" in props
```

---

## 资源测试示例

```python
# tests/unit/test_resources.py
import pytest
from fastmcp import FastMCP


app = FastMCP("Test Server")


@app.resource("config://app")
def get_config() -> dict:
    """返回应用配置"""
    return {"version": "1.0.0", "theme": "dark"}


@app.resource("file://readme")
def get_readme() -> str:
    """返回 README 内容"""
    return "# Test Project\n\nThis is a test."


class TestResources:
    """测试资源"""

    def test_config_resource(self):
        """测试配置资源"""
        resources = app._resource_manager.list_resources()
        config = next(r for r in resources if r.uri == "config://app")

        assert config.name == "get_config"
        assert config.mimeType == "application/json"

    def test_readme_resource(self):
        """测试 README 资源"""
        resources = app._resource_manager.list_resources()
        readme = next(r for r in resources if r.uri == "file://readme")

        assert "readme" in readme.uri
```

---

## Mock 外部依赖

```python
# tests/unit/test_with_mocks.py
import pytest
from unittest.mock import Mock, patch


@app.tool()
def fetch_weather(city: str) -> dict:
    """获取天气信息（依赖外部 API）"""
    import requests
    response = requests.get(f"https://api.weather.com/v3/{city}")
    return response.json()


class TestWithMocks:
    """使用 Mock 测试"""

    @patch('requests.get')
    def test_fetch_weather_success(self, mock_get):
        """测试成功获取天气"""
        mock_response = Mock()
        mock_response.json.return_value = {
            "city": "Beijing",
            "temperature": 22,
            "condition": "Sunny"
        }
        mock_get.return_value = mock_response

        result = fetch_weather(city="Beijing")

        assert result["city"] == "Beijing"
        assert result["temperature"] == 22

    @patch('requests.get')
    def test_fetch_weather_error(self, mock_get):
        """测试 API 错误"""
        import requests
        mock_get.side_effect = requests.HTTPError("API Error")

        with pytest.raises(requests.HTTPError):
            fetch_weather(city="Invalid")
```

---

## 运行测试

```bash
# 运行所有测试
pytest

# 运行特定文件
pytest tests/unit/test_tools.py

# 运行特定测试类
pytest tests/unit/test_tools.py::TestAddTool

# 运行特定测试
pytest tests/unit/test_tools.py::TestAddTool::test_add_positive_numbers

# 显示详细输出
pytest -v

# 显示 print 输出
pytest -s

# 生成覆盖率报告
pytest --cov=src --cov-report=html
```

---

## 测试覆盖率配置

```toml
# pyproject.toml
[tool.coverage.run]
source = ["src"]
omit = ["tests/*", "*/conftest.py"]

[tool.coverage.report]
exclude_lines = [
    "pragma: no cover",
    "def __repr__",
    "raise AssertionError",
    "raise NotImplementedError",
    "if __name__ == .__main__.:",
]
```

---

## 本章小结

1. **测试框架**——pytest 是 Python MCP 测试的主流选择
2. **项目结构**——清晰的测试目录组织
3. **Fixtures**——共享测试数据和设置
4. **工具测试**——完整的工具测试示例
5. **资源测试**——资源定义和返回值测试
6. **Mock**——隔离外部依赖的测试方法
7. **运行命令**——常用的 pytest 命令

---

## 下一步

下一章我们将学习 **集成测试**，测试 MCP 服务器的完整通信流程。

---

*本章贡献者：MCP Tutorial Team*
*版本：v3.0*
