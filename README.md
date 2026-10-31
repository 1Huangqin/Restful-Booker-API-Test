# Restful-Booker API Testing Project
本项目基于开源靶场 Restful-Booker 酒店预订接口系统，使用 Docker 搭建本地测试环境，借助 Postman 完成接口功能测试、自动化回归、边界与安全场景缺陷挖掘，完整覆盖接口用例设计、自动化脚本编写、缺陷提交与生命周期管理流程。

## 🛠️ 技术栈 & 工具
* 测试工具：Postman（Collection Runner 自动化回归）
* 环境部署：Docker，本地访问地址 localhost:3001
* 断言脚本：Postman 内置 JS + Chai 断言库
* 缺陷管理：禅道（Bug提交、跟踪、回归闭环）
* 测试文档：Excel（测试用例）、Word（测试报告）

## 📂 项目目录说明
* Restful-Booker.postman_collection.json：Postman接口集合，内置自动化断言脚本
* Restful-Booker.postman_environment.json：Postman环境变量配置文件
* Restful-Booker接口测试用例.xlsx：共44条测试用例，包含正向流程、CRUD、边界值、异常场景、安全测试（XSS、超长字符串）
* Restful-Booker接口测试报告.docx：汇总测试结果，记录6个核心缺陷
* zentao-bug-list.png：禅道缺陷管理截图，展示Bug全生命周期

## 🚀 项目亮点
1. **接口关联，测试数据闭环**
通过后置脚本自动提取token、bookingid存入环境变量，串联【登录→创建预订→查询→修改→删除】整条业务链路，实现接口自动化串联执行，保证测试数据可控。

2. **自动化断言 & 批量回归**
针对8个核心接口编写24条断言，校验HTTP状态码、返回字段、数据类型、业务返回值；使用Collection Runner一键批量回归，快速验证改动是否引入新问题。

3. **多维度缺陷挖掘**
覆盖功能校验、REST规范、业务逻辑、安全场景，一共发现6个有效缺陷：
- P1严重：缺少业务校验，可创建负数价格脏订单；部分参数缺失导致服务异常
- P2一般：鉴权失败返回200（不符合REST规范）；存在存储型XSS注入风险；PUT全量更新语义不符合规范等

4. **缺陷全流程管理**
将所有缺陷录入禅道，走完激活→开发修复→测试回归→关闭的完整Bug生命周期，模拟企业真实测试流程。

## 💻 如何本地运行 (How to Run)
1. 使用 Docker 启动本地测试环境：
   ```bash
   docker compose up -d
2. 将本仓库中的 postman_collection.json 与 postman_environment.json 导入 Postman。
3. 选中环境变量，打开 Collection Runner 运行测试集合，即可复现自动化测试结果。
