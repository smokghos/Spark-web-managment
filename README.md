
# Web开发-AI 接口文档

本项目提供了一套用于 Web 开发的接口服务，旨在为前后端分离的 Web 应用提供数据支持与业务逻辑处理。接口文档采用 OpenAPI 3.0 标准描述，方便接口调试、测试和集成。以下内容对各模块的接口进行详细说明。

---

## 1. 项目概述

- **名称**：Spark-web-managment  
- **版本**：1.0.0  
- **描述**：本版本文档描述了新版本 Web 开发的接口，通过接口可以实现对班级、部门、员工及报表等数据的管理，以及通用的认证服务。  

---

## 2. 接口分类

接口按照业务领域大致分为以下几大模块：

1. **班级管理**  
   包括班级数据的分页查询、添加、修改、删除和查询所有班级等操作。

2. **部门管理**  
   提供查询所有部门、添加、修改、删除部门以及根据 ID 查询部门等接口。

3. **员工管理**  
   包含员工信息的分页查询、添加、修改、删除、批量删除以及根据 ID 查询员工信息。同时提供查询所有员工数据的接口。

4. **报表统计**  
   目前提供基于员工数据的统计接口，如员工性别统计等。

5. **通用服务**  
   主要提供登录认证接口。用户通过该接口登录后，系统会发放 JWT 令牌，后续请求需要在请求头中携带 token 信息以便验证权限。

---

## 3. 接口详细说明

以下对部分核心接口进行说明，并给出示例参数说明（具体接口参数详见接口文档）：

### 3.1 班级管理接口

- **分页查询班级**  
  - **接口路径**：`GET /clazzs`  
  - **接口说明**：根据班级名称、结课时间区间等条件进行分页查询。  
  - **请求参数示例**：
    - `name`：班级名称（例如 "java就业100期"）
    - `begin`：结课开始时间（例如 "2020-01-01"）
    - `end`：结课结束时间（例如 "2023-01-01"）
    - `page`：页码（例如 1）
    - `pageSize`：每页记录数（例如 10）
  
- **添加班级**  
  - **接口路径**：`POST /clazzs`  
  - **接口说明**：提交包含班级名称、教室、开课、结课时间、班主任 ID 以及所学学科的参数来添加新的班级记录。

- **修改班级**  
  - **接口路径**：`PUT /clazzs`  
  - **接口说明**：修改已存在班级的详细信息，参数参见班级实体定义。

- **删除班级**  
  - **接口路径**：`DELETE /clazzs/{id}`  
  - **接口说明**：通过班级 ID 删除指定班级记录。

- **查询所有班级**  
  - **接口路径**：`GET /clazzs/list`  
  - **接口说明**：无分页条件，返回所有班级数据供下拉框等场景使用。

---

### 3.2 部门管理接口

- **查询所有部门**  
  - **接口路径**：`GET /depts`  
  - **接口说明**：返回部门列表，可在请求头中附带 token 参数验证权限。

- **添加部门**  
  - **接口路径**：`POST /depts`  
  - **接口说明**：新增部门，需传递部门名称。

- **修改部门**  
  - **接口路径**：`PUT /depts`  
  - **接口说明**：根据部门 ID 修改部门信息。

- **删除部门**  
  - **接口路径**：`DELETE /depts`  
  - **接口说明**：根据部门 ID 删除部门记录。
  
- **查询部门详情**  
  - **接口路径**：`GET /depts/{id}`  
  - **接口说明**：通过部门 ID 获取部门的详细信息。

---

### 3.3 员工管理接口

- **分页查询员工**  
  - **接口路径**：`GET /emps`  
  - **接口说明**：可根据姓名、性别及入职日期区间等条件进行分页查询员工列表。  
  - **请求参数示例**：
    - `page`：页码（必填）
    - `pageSize`：每页记录数（必填）
    - `name`：姓名（选填）
    - `gender`：性别（选填，1 表示男，2 表示女）
    - `begin`：入职起始日期（选填）
    - `end`：入职结束日期（选填）

- **添加员工**  
  - **接口路径**：`POST /emps`  
  - **接口说明**：传递员工用户名、姓名、性别、职位、头像、入职日期、部门 ID、薪资以及工作经历列表等数据添加员工。

- **修改员工**  
  - **接口路径**：`PUT /emps`  
  - **接口说明**：根据员工 ID 修改员工信息，包括基本信息和工作经历列表。

- **删除员工（批量删除）**  
  - **接口路径**：`DELETE /emps`  
  - **接口说明**：通过传递多个员工 ID（以逗号分割）实现批量删除。

- **查询所有员工**  
  - **接口路径**：`GET /emps/list`  
  - **接口说明**：返回所有员工信息，适用于无分页需求的场景。

- **通过 ID 查询员工详情**  
  - **接口路径**：`GET /emps/{id}`  
  - **接口说明**：获取指定员工的详细信息，包括工作经历等。

---

### 3.4 登录与通用服务

- **登录接口**  
  - **接口路径**：`POST /login`  
  - **接口说明**：用于员工登录，登录成功后系统下发 JWT 令牌。后续所有受保护接口请求需要在请求头中携带 token。  
  - **请求参数示例**：
    - `username`：用户名（例如 "songjiang"）
    - `password`：密码（例如 "123456"）

---

### 3.5 报表统计接口

- **员工性别统计**  
  - **接口路径**：`GET /report/empGenderData`  
  - **接口说明**：统计并返回不同性别员工的数量，数据以数组形式返回，每个元素包含“性别名称”和“人数”。

- **（其他报表接口说明）**  
  根据完整文档内容，可能还包含其它与员工职位、部门、班级等相关的统计报表接口，可参照实际接口文档补充。

---

## 4. 接口返回格式

所有接口均采用统一的返回数据结构，示例如下：

```json
{
  "code": 1,            // 状态码：1 表示成功，0 表示失败
  "msg": "操作成功",     // 错误提示信息（失败时返回错误描述）
  "data": {             // 接口具体返回数据，可能是对象、数组或字符串
    // 例如：分页查询返回 { total: 100, rows: [...] }
  }
}
```

各接口详细返回字段及示例，可参考对应接口的响应部分。

---

## 5. 使用说明

1. **环境准备**  
   确保您的服务环境支持基于 Java 的后台运行，并配置好相应的数据库以及 JWT 校验机制。

2. **接口调试**  
   可使用 Postman、Swagger UI 或 Apifox 等工具进行接口调试。推荐使用 Apifox 平台（在接口文档中每个接口下均提供线上调试链接）。

3. **权限控制**  
   需要调用受保护接口时，请先使用 `/login` 接口获取 JWT 令牌，并在后续请求头中添加 `token` 参数。

4. **请求示例**  
   每个接口都提供了详细的请求参数和响应示例，请根据实际业务需求传递正确的参数，确保接口调用成功。

---

## 6. 贡献与维护

欢迎各位开发者对本接口文档及后端服务提出建议和优化意见。  
- **提交问题**：如遇到问题，请在 GitHub 上提交 Issue。  
- **代码贡献**：欢迎 Fork 项目，提交 Pull Request 以改进文档或服务实现。  
- **文档更新**：随着业务扩展，接口文档将持续更新完善，请关注最新版本。

---

## 7. 许可协议

本项目接口文档及代码均采用MIT开源协议发布。

---

以上 README 旨在帮助开发者快速了解并使用 Web开发-AI 接口服务。详细接口参数、示例和业务逻辑请参照 OpenAPI 文档及后端代码实现。
