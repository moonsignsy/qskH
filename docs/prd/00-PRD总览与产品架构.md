# 企税康协同工作平台 — PRD 总览与产品架构

| 属性 | 内容 |
|------|------|
| 产品名称 | 企税康协同工作平台 |
| 文档版本 | V1.0 |
| 生成日期 | 2026-05-26 |
| 文档类型 | 产品需求文档（PRD）体系 |
| 原型范围 | D:\Q2 项目全部业务 HTML（31 页，不含 docs 归纳页） |
| 信息架构来源 | `assets/menu-data.js`、`assets/app-shell.js` |

---

## 1. 文档生成流程说明

本次 PRD 严格按以下步骤执行：

| 步骤 | 工作内容 | 产出 |
|------|----------|------|
| Step 1 | 全量阅读项目 HTML 原型（31 个业务页 + login） | 页面功能要素清单 |
| Step 2 | 提取侧栏菜单与详情页归属关系 | 功能模块架构图、页面映射表 |
| Step 3 | 按模块逐功能编写 PRD | 分模块 PRD 文档（见目录） |

**阅读范围说明：**

- 已读：`login.html` 及 menu-data 中全部 31 个业务页面
- 已排除：`docs/企税康协同工作平台-产品全局归纳.html`（归纳文档，非业务页）
- 已删除页面（不在 PRD 范围）：`approval-center.html`、`invoice-management.html`

---

## 2. 产品定位与核心目标

### 2.1 产品定位

面向财税/企服机构的 **B2B 内部协同平台**，覆盖销售获客、客户履约、合同收款、组织运营与系统配置。

### 2.2 核心业务目标

1. **销售增长**：线索→商机→合同→订单全链路数字化
2. **客户履约**：政务、代账、地址、物品等多服务线协同
3. **经营管控**：目标考核、业绩排名、经营报表、报销与人事审批
4. **组织赋能**：员工档案、薪酬、知识库、权限与字典配置
5. **管理驾驶舱**：工作台聚合 KPI、待办、排行与业务速览

### 2.3 目标用户角色

| 角色 | 典型使用模块 |
|------|-------------|
| 销售顾问 | 线索、商机、客户、合同、工作台 |
| 销售主管 | 销售目标、销售业绩、团队排行 |
| 政务/代账经办 | 政务服务、代账服务 |
| 财务 | 订单、报销、薪资、经营报表 |
| 人事/行政 | 人事管理、员工管理 |
| 管理层 | 工作台、经营报表、业绩排名 |
| 系统管理员 | 角色权限、字典、菜单管理 |

---

## 3. 功能模块架构

### 3.1 一级模块树（来自 menu-data.js）

```
企税康协同工作平台
├── 入口
│   └── login.html
├── 1. 工作台 (index.html)
├── 2. 销售管理
│   ├── sales-target.html          销售目标
│   ├── lead-management.html       线索管理
│   ├── lead-follow-detail.html    跟进日志详情 [详情]
│   ├── opportunity-management.html 商机管理
│   ├── opportunity-detail.html    商机详情 [详情]
│   └── sales-performance.html     销售业绩
├── 3. 客户中心
│   ├── customer-management.html   客户管理
│   ├── customer-detail.html       客户详情 [详情]
│   ├── customer-edit.html         编辑客户 [详情]
│   ├── government-affairs.html    政务服务
│   ├── government-affairs-detail.html 工单详情 [详情]
│   ├── accounting-customer-management.html 代账服务
│   ├── accounting-customer-detail.html 代账详情 [详情]
│   ├── address-management.html    地址管理
│   ├── address-room-detail.html   地址详情 [详情]
│   └── customer-items.html        客户物品
├── 4. 知识库 (knowledge-base.html)
├── 5. 合同订单
│   ├── contract-management.html   合同管理
│   └── order-management.html      订单管理
├── 6. 运营管理
│   ├── payment-request.html       财务报销
│   ├── financial-reports.html     经营报表
│   ├── hr-request.html            人事管理
│   ├── salary-management.html     薪资管理
│   ├── department-employees.html  员工管理
│   ├── employee-profile.html      员工档案 [详情]
│   └── employee-edit.html         员工信息编辑 [详情]
└── 7. 系统管理
    ├── role-permissions.html      角色权限
    ├── dictionary-management.html 字典管理
    └── menu-management.html       菜单管理
```

### 3.2 详情页侧栏归属（DETAIL_PARENT）

| 详情页 | 高亮列表页 |
|--------|-----------|
| customer-detail / customer-edit | customer-management |
| lead-follow-detail | lead-management |
| opportunity-detail | opportunity-management |
| government-affairs-detail | government-affairs |
| accounting-customer-detail | accounting-customer-management |
| address-room-detail | address-management |
| employee-profile / employee-edit | department-employees |

### 3.3 共享组件

| 组件 | 路径 | 挂载页面 |
|------|------|----------|
| 创建合同弹窗 | assets/create-contract-modal.js | index、customer-management、contract-management、opportunity-management |
| 应用壳层 | assets/app-shell.js | 除 login 外全部业务页 |
| 菜单配置 | assets/menu-data.js | menu-management 可覆盖 |

---

## 4. 核心业务链路

### 4.1 销售成单链路

```
login → 工作台
  → 线索管理 → [转商机] → 商机管理
  → 创建合同 → 合同管理 → 订单管理 → 开票/收款
  → 销售目标 / 销售业绩（考核反馈）
```

### 4.2 客户履约链路

```
客户管理（主数据）
  ├─ 客户详情 → 服务详情 / 档案 / 维护 / 跟进
  ├─ 政务服务 → 工单详情
  ├─ 代账服务 → 代账详情
  ├─ 地址管理 → 房间详情
  └─ 客户物品
```

### 4.3 运营审批链路

```
财务报销 / 人事管理
  → 我提交 / 待我处理 / 已处理 / 抄送
  → 审批详情 → 通过/拒绝/撤销/确认支付
```

---

## 5. PRD 文档目录

| 编号 | 文档 | 覆盖页面 |
|------|------|----------|
| 00 | 本文档 | 架构总览 |
| 01 | [01-登录与工作台-PRD.md](./01-登录与工作台-PRD.md) | login、index |
| 02 | [02-销售管理-PRD.md](./02-销售管理-PRD.md) | 销售目标、线索、商机、业绩（6页） |
| 03 | [03-客户中心-PRD.md](./03-客户中心-PRD.md) | 客户、政务、代账、地址、物品（10页） |
| 04 | [04-知识库-PRD.md](./04-知识库-PRD.md) | knowledge-base |
| 05 | [05-合同订单-PRD.md](./05-合同订单-PRD.md) | contract、order |
| 06 | [06-运营管理-PRD.md](./06-运营管理-PRD.md) | 报销、报表、人事、薪资、员工（7页） |
| 07 | [07-系统管理-PRD.md](./07-系统管理-PRD.md) | 权限、字典、菜单 |

---

## 6. 全局非功能需求

| 类别 | 要求 |
|------|------|
| 终端适配 | 侧栏移动端抽屉；表格横向滚动 |
| 交互一致性 | 筛选面板、弹窗、Tab 样式统一（design-system.css） |
| 权限 | 由 role-permissions 模块控制菜单与操作 |
| 数据 | 当前为静态原型；正式版需 API + 鉴权 |
| 字符限制 | 多处表单有长度校验（如姓名5、手机11、跟进1000） |

---

## 7. 版本记录

| 版本 | 日期 | 说明 |
|------|------|------|
| V1.0 | 2026-05-26 | 基于全量 HTML 原型首次生成 PRD 体系 |
