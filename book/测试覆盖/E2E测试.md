# E2E 测试指南

> 模拟真实用户场景的端到端测试

---

## E2E 测试策略

```
┌─────────────────────────────────────────────────────────────────┐
│                    E2E 测试覆盖范围                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  用户视角                                                        │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  1. 启动 MCP 服务器                                     │   │
│  │  2. 配置 Claude Desktop / Cursor                       │   │
│  │  3. 发起用户请求                                        │   │
│  │  4. MCP 服务器处理请求                                  │   │
│  │  5. 返回结果给 AI                                       │   │
│  │  6. AI 生成响应                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 使用 Playwright 进行 E2E 测试

### 安装

```bash
pip install playwright pytest-playwright
playwright install chromium
```

### 基础 E2E 测试

```python
# tests/e2e/test_mcp_client.py
import pytest
from playwright.sync_api import sync_playwright


class TestMCPE2E:
    """MCP E2E 测试"""

    @pytest.fixture(autouse=True)
    def setup(self):
        """测试设置"""
        self.playwright = sync_playwright().start()
        self.browser = self.playwright.chromium.launch(headless=True)
        self.context = self.browser.new_context()
        self.page = self.context.new_page()

        yield

        self.browser.close()
        self.playwright.stop()

    def test_mcp_file_operations(self):
        """测试 MCP 文件操作"""
        # 模拟用户操作：让 AI 操作文件
        # 注意：这是简化的示例，实际需要完整配置
        self.page.goto("claude.ai")

        # 输入请求
        self.page.fill('textarea', '请列出桌面的文件')

        # 等待响应（简化）
        self.page.wait_for_timeout(2000)

        # 验证结果
        content = self.page.text_content('body')
        assert content is not None
```

---

## 模拟 MCP 交互

```python
# tests/e2e/test_mcp_simulation.py
import pytest
import subprocess
import json
import time


class TestMCPSimulation:
    """模拟 MCP 客户端的 E2E 测试"""

    @pytest.fixture
    def mcp_server(self):
        """启动 MCP 服务器"""
        process = subprocess.Popen(
            ["python", "-m", "my_mcp_server"],
            stdout=subprocess.PIPE,
            stderr=subprocess.PIPE,
            text=True
        )

        # 等待服务器启动
        time.sleep(2)

        yield process

        # 清理
        process.terminate()
        process.wait()

    def test_json_rpc_roundtrip(self, mcp_server):
        """测试完整的 JSON-RPC 交互"""
        # 构建 JSON-RPC 请求
        request = {
            "jsonrpc": "2.0",
            "id": 1,
            "method": "tools/call",
            "params": {
                "name": "add",
                "arguments": {"a": 5, "b": 3}
            }
        }

        # 发送请求（简化示例）
        # 实际测试中需要完整的 MCP 客户端实现
        print(f"Sending: {json.dumps(request)}")

        # 验证响应
        # assert response["result"] is not None
```

---

## 场景化 E2E 测试

```python
# tests/e2e/test_scenarios.py
import pytest


class TestRealWorldScenarios:
    """真实世界场景测试"""

    async def test_github_pr_workflow(self, session):
        """
        场景：GitHub PR 审查工作流

        步骤：
        1. 获取仓库的 PR 列表
        2. 选择一个 PR
        3. 获取 PR 的变更内容
        4. 生成审查意见
        5. 添加评论
        """
        # Step 1: 获取 PR 列表
        prs = await session.call_tool(
            name="github_list_prs",
            arguments={"owner": "test-org", "repo": "test-repo"}
        )

        if not prs.content:
            pytest.skip("No PRs available")

        # Step 2: 获取第一个 PR 的详情
        pr_number = prs.content[0].text.split("#")[1].split()[0]
        pr_detail = await session.call_tool(
            name="github_get_pr",
            arguments={"owner": "test-org", "repo": "test-repo", "pr_number": pr_number}
        )

        # Step 3: 获取变更内容
        diff = await session.call_tool(
            name="github_get_pr_diff",
            arguments={"owner": "test-org", "repo": "test-repo", "pr_number": pr_number}
        )

        # Step 4-5: 添加审查评论（模拟）
        # 实际场景中，AI 会分析 diff 并生成评论
        comment = await session.call_tool(
            name="github_create_review_comment",
            arguments={
                "owner": "test-org",
                "repo": "test-repo",
                "pr_number": pr_number,
                "body": "代码审查意见：建议添加类型注解"
            }
        )

        assert comment.content[0].type == "text"

    async def test_database_query_workflow(self, session):
        """
        场景：数据库查询工作流

        步骤：
        1. 连接数据库
        2. 执行查询
        3. 格式化结果
        4. 生成报告
        """
        # Step 1: 连接数据库
        conn = await session.call_tool(
            name="db_connect",
            arguments={"connection_string": "sqlite:///test.db"}
        )

        # Step 2: 执行查询
        result = await session.call_tool(
            name="db_query",
            arguments={"sql": "SELECT * FROM users LIMIT 10"}
        )

        # 验证结果
        assert result.content[0].type == "text"
        assert "users" in result.content[0].text.lower()
```

---

## E2E 测试最佳实践

```
┌─────────────────────────────────────────────────────────────────┐
│                    E2E 测试最佳实践                              │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  1. 独立性                                                      │
│     └── 每个测试应该能够独立运行                                 │
│                                                                 │
│  2. 幂等性                                                      │
│     └── 测试可以重复运行而不产生副作用                           │
│                                                                 │
│  3. 清晰的断言                                                  │
│     └── 明确验证预期结果                                        │
│                                                                 │
│  4. 适当的超时                                                  │
│     └── 考虑网络延迟和外部服务响应时间                           │
│                                                                 │
│  5. 测试数据隔离                                                │
│     └── 使用测试数据库或 mock 外部依赖                          │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 本章小结

1. **E2E 概念**——从用户视角测试完整流程
2. **Playwright**——浏览器自动化测试
3. **JSON-RPC 模拟**——直接测试协议交互
4. **场景测试**——真实工作流测试
5. **最佳实践**——独立性、幂等性、清晰断言

---

## 下一步

下一章我们将配置 **CI/CD**，实现自动化测试和部署。

---

*版本：v3.0*
