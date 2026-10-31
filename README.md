# Restful-Booker API Automation Testing

本项目基于开源靶场 Restful-Booker 酒店预订系统，使用 Docker、Postman 进行接口自动化测试与缺陷挖掘。项目涵盖了接口用例设计、自动化脚本编写、环境部署以及缺陷的全生命周期管理。

## 🛠️ 技术栈 & 工具
*   **测试工具**：Postman (Collection Runner)
*   **环境部署**：Docker (Localhost:3001)
*   **断言框架**：Chai (Postman内置 JS 脚本)
*   **缺陷管理**：禅道
*   **文档管理**：Excel, Word

## 📂 项目目录说明
*   `Restful-Booker.postman_collection.json`：Postman 接口集合（含 24 个自动化断言脚本）
*   `Restful-Booker.postman_environment.json`：Postman 环境变量配置
*   `Restful-Booker接口测试用例.xlsx`：44 条接口测试用例（涵盖鉴权、CRUD、边界值、异常流）
*   `Restful-Booker接口测试报告.docx`：包含 6 个核心缺陷详细描述的综合测试报告
*   `zentao-bug-list.png`：6 个核心缺陷在禅道中全生命周期闭环截图

## 🚀 核心产出 & 测试亮点
1.  **接口关联与数据闭环**：利用 `Post-response Script` 动态提取 Token 与 Booking ID 并存入环境变量。实现了“创建->修改->删除”的自动化数据闭环，确保测试数据隔离，不污染原有数据库。
2.  **自动化断言**：覆盖 8 个核心接口，编写了 24 个自动化断言（校验状态码、响应体字段、数据类型等）。通过 Collection Runner 批量回归，断言通过率 100%。
3.  **深入的缺陷挖掘**：累计发现并定位 6 个有效缺陷，包含：
    *   **P1级 (严重)**：缺失必填参数导致服务端 500 崩溃、业务规则缺失允许生成负数金额脏订单。
    *   **P2级 (一般)**：鉴权失败返回 200 状态码（违反 RESTful 规范）、未过滤特殊字符存在存储型 XSS 风险等。
4.  **缺陷闭环管理**：将 6 个核心缺陷提交至禅道，并完成从“激活”到“解决”再到“回归关闭”的完整生命周期跟踪。

## 💻 如何本地运行 (How to Run)
1. 使用 Docker 启动本地测试环境：
   ```bash
   docker compose up -d```
2. 将本仓库中的 postman_collection.json 与 postman_environment.json 导入 Postman。
3. 选中环境变量，打开 Collection Runner 运行测试集合，即可复现自动化测试结果。
