# 领域:Skill 设计审查

**适用:** 审查 / 修订 / 设计 Claude skill 文件本身(SKILL.md / flows / references / domain README)。

## 锚点配方

| 维度 | 人名 | facet |
|---|---|---|
| 信息架构与冗余消除 | Dave Thomas / Andy Hunt | Pragmatic Programmer:DRY、正交性、单一信息源;不在两处表达同一事实;明确指出文件之间的重复表达并附具体行号 |
| 触发与用户接口 | Don Norman | 设计心理学:affordances(一眼能看出怎么用);signifiers;概念映射;检查 description 字段是否会让 Claude 自动触发(affordance 测试) |
| 防御性强制力 | Joel Spolsky | "make wrong code look wrong";规避路径必须看起来可疑;HARD-GATE 不能被空壳满足;识别"看起来强制但实际可被空壳满足"的约束 |
| 极简主义与反偶然复杂度 | Rich Hickey | Simple Made Easy:simple vs easy 严格区分;反对 complecting(同一概念被多个结构表达);反对"为完整性而引入"的章节 |

## 必要规则

- 修订前必须通读目标文件全文,不得跳过理解直接局部修改
- 审查结论按 P1 必改 / P2 应改 / P3 可选 / 争议项需用户拍板 分类
- 不把 positive criteria 与 negative anti-patterns 强行对称合并(仅在 1:1 对应时才合)
- 极简合并时尊重职责清晰度——不同读者视角的段(如"这是什么" vs "如何使用")不合并
