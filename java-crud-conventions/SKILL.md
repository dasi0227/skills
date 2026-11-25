---
name: java-crud-conventions
description: 在 Java Spring 项目中实现、修改或审查 CRUD 功能时使用，按项目约定处理接口契约、分层对象转换、写入校验和事务。
---

# Spring CRUD 规范

- Controller、Service、Repository 和 Mapper 的方法名应明确表达操作及其对象。
- 查询接口统一使用 `@GetMapping`，创建、更新和删除接口统一使用 `@PostMapping`。
- 查询参数通过 `@PathVariable` 或 `@RequestParam` 接收，写入参数通过 `@Valid @RequestBody` 接收。
- 创建接口统一返回 `IdVo`，更新接口统一返回 `void`，前端按需重查最新数据。
- 详情 VO 统一命名为 `XxxInfoVo`，列表 VO 统一命名为 `XxxListVo`。
- 仅供一个 VO 使用的子 VO，可定义为该 VO 的静态嵌套类。
- VO 字段禁止使用 `@JsonInclude`，空值的返回形式由前后端在接口契约中明确约定。
- DTO 转领域对象的方法统一命名为 `toEntity()`，定义在对应 DTO 中。
- 领域对象转 VO 的方法统一命名为 `toVo()`，定义在目标 VO 中。
- 领域对象转 PO 的方法统一命名为 `toPo()`，集中放在 Repository 类的底部。
- PO 转领域对象的方法统一命名为 `toEntity()`，集中放在 Repository 类的底部，并以 `if (po == null) return null;` 作为首条语句。
- 读取完整记录时，Mapper 返回 `XxxPo` 或 `List<XxxPo>`，由 Repository 转为对应的领域实体或实体列表。仅查询单个值时，Mapper 直接按该值的类型返回。
- 创建资源、整组保存或更新多个可选字段时，Repository 将领域实体转为 PO 后交给 Mapper 写入。枚举与字符串、列表与 JSON 之间的双向转换均由 Repository 负责。
- 删除、改名和批量关联等简单操作由 Repository 直接向 Mapper 传入操作所需的参数，无需组装 PO。
- 创建资源时由后端生成 ID 并设置适用的初始状态和时间戳，创建 DTO 不接收 ID，更新 DTO 通常须提供目标资源 ID。
- 当 ID 足以唯一定位资源时，请求仅提交 ID 和本次操作所需字段，校验所需的类型等不可变属性由后端按 ID 读取。
- 字段的非 `null`、非空、非空白、长度和格式约束统一通过 DTO 上的 Jakarta Validation 注解声明。
- Controller、Service 和 Repository 仅保留接口契约、业务规则和数据一致性所需的检查，禁止针对假想非法输入增加防御性校验或重复校验。
- Service 应在对应业务方法中按执行顺序逐项完成写入前校验，禁止抽取公共校验方法。
- Repository 的单条查询未命中时可返回 `null`，列表查询无结果时统一返回空集合。
- Repository 负责返回数据访问结果，`NOT_FOUND` 等业务错误统一由 Service 判定并抛出。
- 更新或删除的影响行数足以判断资源是否存在时，Repository 直接返回行数，由 Service 在写入后判断，省去额外的 `exists` 查询。
- Service 通过 `@Transactional` 划定写事务，使同一操作涉及的主表、关联表和受影响资源一并提交或回滚。
- Controller 按资源分组并在组内依次排列列表、详情、创建、更新和删除方法，Service 的公开方法与对应 Controller 保持同序。
- 对有唯一性要求的字段，创建和更新应按相同的业务范围查重，更新时排除当前资源，允许提交原值。
- 局部更新时，省略或显式传 `null` 的可选字段在 PO 中均保留为 `null`，表示保留原值。可选布尔字段使用 `Boolean`。Mapper 仅对非 `null` 的可选字段生成赋值，`0` 和 `false` 均按传入值写入。动态 `SET` 子句固定包含 `id = id`，支持仅传 ID 的更新。
- 创建和更新时，Service 在调用 Repository 前设置实体的 `updatedAt`，两条路径共用 `toPo()` 原样映射该值。每次更新时，数据库取传入值与 `updated_at + 1` 的较大值，保证时间戳严格递增。
- 同一作用域内可创建多份的资源使用 `create`，作用域内只有一份的配置使用 `save`，支持修改时使用 `update`，查询列表使用 `list`。
- DTO、VO、PO 和领域实体统一使用普通类，禁止使用 `record`。DTO、VO 和 PO 均使用 Lombok 的 `@Builder`、`@Getter`、`@AllArgsConstructor` 和 `@NoArgsConstructor`。领域实体统一使用 `@Data`。
