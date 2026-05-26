# PRD — 客户中心

| 属性 | 内容 |
|------|------|
| 模块 | 客户中心 |
| 页面 | 10 页（含 5 详情/编辑） |
| 优先级 | P0 |
| 版本 | V1.0 |

---

## 1. 模块概述

以客户主数据为核心，串联政务、代账、地址、物品等多服务线履约管理，支撑销售与经办协同。

---

## 2. 页面清单

| 页面 | 类型 | 文件 |
|------|------|------|
| 客户管理 | 列表 | customer-management.html |
| 客户详情 | 详情 | customer-detail.html |
| 编辑客户 | 编辑 | customer-edit.html |
| 政务服务 | 列表 | government-affairs.html |
| 工单详情 | 详情 | government-affairs-detail.html |
| 代账服务 | 列表 | accounting-customer-management.html |
| 代账详情 | 详情 | accounting-customer-detail.html |
| 地址管理 | 列表 | address-management.html |
| 地址详情 | 详情 | address-room-detail.html |
| 客户物品 | 列表 | customer-items.html |

---

## 3. 客户管理（customer-management.html）

### 3.1 筛选

| 字段 | 类型 |
|------|------|
| 客户名称 | 文本 |
| 联系人/联系方式 | 文本 |
| 企业类型 | 下拉 |
| 销售顾问 | 下拉 |
| 代账客户 | 全部/是/否 |
| 主办会计 | 下拉 |
| 创建时间 | 日期区间 |

> 说明：已移除「合作状态」筛选项与列表列。

### 3.2 列表字段

勾选、客户名称、联系人、联系方式、企业类型、销售顾问、代账客户、主办会计、创建时间、查看详情、操作

### 3.3 操作

- 新增合同（`js-open-create-contract`，共用 create-contract-modal.js）
- 编辑信息 → customer-edit.html?id=cust-{n}
- 查看详情 → customer-detail.html?id=cust-{n}
- 全部导出

---

## 4. 客户详情（customer-detail.html）

### 4.1 布局

- 顶部：返回列表、服务状态标签
- 流程步骤条（客户服务流程）
- 左 3/5：Tab 主内容
- 右 2/5：客户摘要 + 快捷操作

### 4.2 Tab 结构

| Tab | 内容 |
|-----|------|
| 服务详情 | 代理记账/注册地址/增值服务等卡片，含套餐、截止月份、经办人、查看合同 |
| 客户档案 | 基本信息、工商信息、附件资料 |
| 客户维护记录 | 时间轴（维护类型、内容、维护人） |
| 销售跟进记录 | 跟进时间轴 |

### 4.3 弹窗

| 弹窗 | 用途 |
|------|------|
| modal-quote-preview | 报价单预览 |
| modal-add-maintain | 添加客户维护 |

### 4.4 路由

- `?id=cust-1~n` 驱动客户数据
- 侧栏高亮 customer-management（DETAIL_PARENT）

---

## 5. 编辑客户（customer-edit.html）

- 表单编辑客户基本信息与工商信息
- 保存后返回详情或列表
- 侧栏高亮 customer-management

---

## 6. 政务服务（government-affairs.html）

### 6.1 筛选

企业名称、业务类型、所属区域、办理状态、销售顾问、经办人、派单时间/完成日期/创建时间区间

### 6.2 Tab

全部 / 办理中 / 已完成

### 6.3 列表字段

企业名称、业务类型、区域、销售顾问、部门、线上申报员、线下提报员、客户资料、接收资料时间、已办理天数（颜色徽章）、派单时间、完成日期、查看详情、操作

### 6.4 行操作（随状态）

| 状态 | 操作 |
|------|------|
| 未派单 | 派单 |
| 办理中 | 添加进度、移交 |
| 已完成 | 查看详情 |

### 6.5 弹窗

| 弹窗 | 用途 |
|------|------|
| modal-new-order | 新建政务工单 |
| modal-dispatch | 派单（线上/线下申报员） |
| modal-progress | 添加办理进度 |
| modal-transfer-gov | 移交 |

### 6.6 外链

→ government-affairs-detail.html?id=gov-{n}

---

## 7. 工单详情（government-affairs-detail.html）

- 工单基本信息网格
- 办理进度时间轴
- 附件/资料区
- 上一条/下一条导航
- `?id=gov-{n}` 驱动

---

## 8. 代账服务（accounting-customer-management.html）

### 8.1 筛选

企业名称、服务状态、企业类型、主办会计、财税顾问、代账到期、创建时间区间

### 8.2 Tab

全部 / 服务中 / 已到期 / 已终止

### 8.3 列表字段

企业名称、企业类型、服务套餐、主办会计、财税顾问、销售顾问、服务状态、代账到期、创建时间、查看详情、操作

### 8.4 弹窗

| 弹窗 | 用途 |
|------|------|
| modal-add-accounting | 添加代账客户 |
| modal-dispatch-accounting | 派单（主办会计/财税顾问） |
| modal-progress-accounting | 添加服务进度 |
| modal-transfer-accounting | 移交 |

### 8.5 外链

→ accounting-customer-detail.html?id=acc-{n}

---

## 9. 代账详情（accounting-customer-detail.html）

- 代账服务信息、记账周期、人员配置
- 服务进度时间轴
- 续费/到期提醒
- `?id=acc-{n}` 驱动

---

## 10. 地址管理（address-management.html）

### 10.1 布局

- 左侧：园区/楼宇树形结构
- 右侧：房间列表

### 10.2 列表字段

房间号、面积、状态（空闲/已租/预留）、关联客户、租赁截止、操作

### 10.3 弹窗

| 弹窗 | 用途 |
|------|------|
| modal-add-address | 添加/编辑地址房间 |
| modal-delete | 删除确认 |

### 10.4 外链

→ address-room-detail.html?id=room-{n}

---

## 11. 地址详情（address-room-detail.html）

- 房间基本信息、租赁历史
- 当前租户信息
- 关联合同链接

---

## 12. 客户物品（customer-items.html）

### 12.1 筛选

客户名称、物品类型、存放位置、状态

### 12.2 列表字段

客户名称、物品名称、类型、数量、存放位置、登记人、登记时间、操作

### 12.3 弹窗

| 弹窗 | 用途 |
|------|------|
| modal-add-item | 登记物品 |
| modal-transfer-item | 物品移交（给客户） |
| modal-internal-transfer | 内部转交 |

---

## 13. 模块业务流程

```
客户管理（主数据）
  ├─ 客户详情 ←→ 编辑客户
  ├─ 新增合同 → 合同管理
  ├─ 政务服务 → 派单/进度 → 工单详情
  ├─ 代账服务 → 派单/进度 → 代账详情
  ├─ 地址管理 → 房间详情
  └─ 客户物品 → 登记/移交
```

---

## 14. 验收标准

- [ ] 客户列表无合作状态字段，主办会计文案正确
- [ ] 客户详情 4 Tab 切换正常
- [ ] 政务/代账 Tab 过滤与行操作正确
- [ ] 地址树与房间列表联动
- [ ] 物品登记与移交弹窗可用
- [ ] 详情页 URL 参数切换数据
