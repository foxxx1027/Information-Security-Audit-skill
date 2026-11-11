# 06-管理与流程合规 · 管理与流程合规审计 —— 技能说明

## 本目录审计范围

审计范围：账号生命周期、权限审批、变更发布流程、上线安全测试、应急响应、备份恢复演练、安全制度、等保/数据安全合规、数据最小化、脱敏、数据出境、隐私合规。

## 技能清单（36 个）

| 集合 | 技能 | 一句话说明 | 归类理由 |
|---|---|---|---|
| Web应用防御 | `whitehat-data-classification-modules`<br>[数据定级模块化保护](../../skills/webapp-defense/whitehat-data-classification-modules/SKILL.md) | 访谈定级数据，按级定义保护方式并模块化复用，统一多项目安全标准 | 数据分级治理与标准复用流程 |
| Web应用防御 | `whitehat-data-minimization`<br>[数据最小化原则](../../skills/webapp-defense/whitehat-data-minimization/SKILL.md) | 先问要不要持有再谈怎么保护：采集/存储/留存全链减量，不存即零泄露 | 数据持有面治理与隐私合规落地 |
| Web应用防御 | `whitehat-requirement-decomposition`<br>[安全需求分解](../../skills/webapp-defense/whitehat-requirement-decomposition/SKILL.md) | 把更安全口号拆成可判定威胁条目再对齐验收标准，可验收才可交付 | SDL需求阶段流程与验收对齐 |
| Web应用防御 | `whitehat-security-as-compliance-checks`<br>[安全合规化检查](../../skills/webapp-defense/whitehat-security-as-compliance-checks/SKILL.md) | 把安全吗开放命题转为可判定合规条目并映射可扫描信号，CI门禁落地 | 规范制度落地为可检查条目流程 |
| Web应用防御 | `whitehat-security-process-fit-delivery-cadence`<br>[流程适配交付节奏](../../skills/webapp-defense/whitehat-security-process-fit-delivery-cadence/SKILL.md) | 安全机制存亡取决于与交付节奏兼容性，错配流程被无声绕过防护归零 | SDL流程落地节奏设计 |
| Web应用防御 | `whitehat-solution-acceptance-checklist`<br>[方案验收五条清单](../../skills/webapp-defense/whitehat-solution-acceptance-checklist/SKILL.md) | 按有效/体验/性能/耦合/扩展五维评审安全方案，体验与性能一票否决 | 安全方案合格性的验收流程 |
| 体系审核验证 | `isms-auditor-independence-checks`<br>[审核员独立性核查](../../skills/system-audit-verification/isms-auditor-independence-checks/SKILL.md) | 审核组分工回避、咨询顾问两年回避、技术专家仅建议不算审核员 | 审核人员独立性与回避程序 |
| 体系审核验证 | `isms-combined-audit-admission`<br>[结合审核准入判定](../../skills/system-audit-verification/isms-combined-audit-admission/SKILL.md) | 三条件硬门槛加机制同构判定，决定多标准能否一次进场合审 | 结合审核可行性与底线准入 |
| 体系审核验证 | `isms-combined-audit-planning-calibration`<br>[结合审核策划校准](../../skills/system-audit-verification/isms-combined-audit-planning-calibration/SKILL.md) | 用业务、职责、文件三类客观材料校准整合自述，定路径与人日 | 整合审核策划与阶段校准 |
| 体系审核验证 | `isms-common-difference-evidence-split`<br>[共同差异点取证分配](../../skills/system-audit-verification/isms-common-difference-evidence-split/SKILL.md) | 共同关注点合并取证、差异点逐标准单查，防独有要求被稀释 | 多标准合并检查表与取证分工 |
| 体系审核验证 | `isms-control-equivalence-judgment`<br>[控制等效性判定](../../skills/system-audit-verification/isms-control-equivalence-judgment/SKILL.md) | 控制做不到时改审等效达成：提炼目标、识别补偿措施、查运行证据 | 补偿性控制等效判定方法 |
| 体系审核验证 | `isms-counterfactual-document-review`<br>[反证式文件审读](../../skills/system-audit-verification/isms-counterfactual-document-review/SKILL.md) | SMART与5W1H各挂失效后果链，用缺了会坏什么审承诺类文本 | 承诺文本可审计性评审方法 |
| 体系审核验证 | `isms-degraded-evidence-fallback`<br>[降级证据处理](../../skills/system-audit-verification/isms-degraded-evidence-fallback/SKILL.md) | 数据未到期时以约定加配置层证据替代，声明降级并约期复核 | 证据降级与限定结论程序 |
| 体系审核验证 | `isms-document-consistency-matrix`<br>[文件一致性核对矩阵](../../skills/system-audit-verification/isms-document-consistency-matrix/SKILL.md) | 四组一致性关系核对程序与产出物，识破表演性文件 | 文件评审四查，体系文件互证 |
| 体系审核验证 | `isms-evidence-admissibility-threshold`<br>[证据资格三门槛](../../skills/system-audit-verification/isms-evidence-admissibility-threshold/SKILL.md) | 相关、可证实、已记录三道门槛，听说与口头承诺只算线索 | 通用取证思维，划线索与证据 |
| 体系审核验证 | `isms-four-column-checklist-design`<br>[四栏检查表设计](../../skills/system-audit-verification/isms-four-column-checklist-design/SKILL.md) | shall转检查题、答案二值附理由，外来通用表必裁剪后用 | 检查表题型结构设计规范 |
| 体系审核验证 | `isms-interview-questioning-discipline`<br>[访谈提问纪律](../../skills/system-audit-verification/isms-interview-questioning-discipline/SKILL.md) | 面谈八注意防引导性提问，请对方描述工作、结尾总结评审 | 取证访谈现场提问纪律 |
| 体系审核验证 | `isms-interview-tiering`<br>[访谈分层选档](../../skills/system-audit-verification/isms-interview-tiering/SKILL.md) | 按结论层级选访谈对象与深度，存在层取样不得下有效性结论 | 访谈对象与深度规划设计 |
| 体系审核验证 | `isms-multi-site-sampling-formula`<br>[多场所抽样公式](../../skills/system-audit-verification/isms-multi-site-sampling-formula/SKILL.md) | 先过相似性闸门再按平方根乘风险系数定样本量，总部必查 | 多场所审核抽样方案设计 |
| 体系审核验证 | `isms-nonconformity-grading-loop`<br>[不符合项分级闭环](../../skills/system-audit-verification/isms-nonconformity-grading-loop/SKILL.md) | 重大、一般、观察项三级判据，验证纠正有效性后方可关单 | 不符合项定级与整改闭环 |
| 体系审核验证 | `isms-risk-acceptance-criteria-first`<br>[风险接受准则先行](../../skills/system-audit-verification/isms-risk-acceptance-criteria-first/SKILL.md) | 先查接受标准是否先于处置存在，残余风险须管理者正式批准 | 风险处置与接受标准治理 |
| 体系审核验证 | `isms-sampling-uncertainty-disclosure`<br>[抽样不确定性披露](../../skills/system-audit-verification/isms-sampling-uncertainty-disclosure/SKILL.md) | 首末次会议告知加报告载明局限，结论限定为样本未见不符合 | 抽样结论边界与报告披露 |
| 体系审核验证 | `isms-soa-justification-traceback`<br>[SoA说理回溯](../../skills/system-audit-verification/isms-soa-justification-traceback/SKILL.md) | 双向抽查控制选删理由，清单齐全非合规证据，断链即发现 | 适用性声明选控说理审查 |
| 体系审核验证 | `isms-two-stage-audit-gate`<br>[两阶段审核门禁](../../skills/system-audit-verification/isms-two-stage-audit-gate/SKILL.md) | 一阶段换信息与判断，五类门槛问题整改完毕方可进二阶段 | 分阶段审核放行门禁设计 |
| 体系审核验证 | `isms-two-step-conformity-audit`<br>[两步符合性审核](../../skills/system-audit-verification/isms-two-step-conformity-audit/SKILL.md) | 先查过程存在性再逐条查shall符合，防文件符合掩盖过程缺失 | 条款符合性判定总顺序 |
| 合规测评 | `mlps-compliance-vs-risk-boundary`<br>[等级测评与风险评估的分工边界](../../skills/compliance-assessment/mlps-compliance-vs-risk-boundary/SKILL.md) | 等级测评评措施、风险评估评威胁，结论措辞与合同边界 | 合规与风险结论边界 |
| 合规测评 | `mlps-deliverable-stage-gates`<br>[产物驱动的阶段管理与节点评审冻结](../../skills/compliance-assessment/mlps-deliverable-stage-gates/SKILL.md) | 阶段完成以产物清单为准，方案经确认后评审冻结 | 项目阶段流程管理 |
| 合规测评 | `mlps-delivery-completeness-check`<br>[交付完整性核查](../../skills/compliance-assessment/mlps-delivery-completeness-check/SKILL.md) | 按物纸人责四要素核查交付移交，追讨过程性文档债务 | 系统交付完整性管理 |
| 合规测评 | `mlps-document-lifecycle-closed-loop`<br>[文档闭环管理](../../skills/compliance-assessment/mlps-document-lifecycle-closed-loop/SKILL.md) | 以评审修订掌握度三证据判断制度文档是否仍被运营 | 文档闭环管理 |
| 合规测评 | `mlps-go-live-quality-gate`<br>[建设期质量门](../../skills/compliance-assessment/mlps-go-live-quality-gate/SKILL.md) | 第三方独立测试加四件套覆盖与外包后门审查的放行门 | 上线验收质量门 |
| 合规测评 | `mlps-grading-decision`<br>[等保定级决策程序](../../skills/compliance-assessment/mlps-grading-decision/SKILL.md) | 受侵害客体乘侵害程度双要素定级，S/A取高加三方校验 | 定级是合规动作 |
| 合规测评 | `mlps-management-root-cause-traceback`<br>[管理根因回溯法](../../skills/compliance-assessment/mlps-management-root-cause-traceback/SKILL.md) | 技术整改无效时沿制度归口、职责闭合、人员链回溯根因 | 管理根因追溯 |
| 合规测评 | `mlps-personnel-lifecycle-controls`<br>[人员安全全生命周期管控](../../skills/compliance-assessment/mlps-personnel-lifecycle-controls/SKILL.md) | 录用在职离岗外部人员四阶段管控，离岗三步收权 | 人员全周期安全管理 |
| 合规测评 | `mlps-policy-four-layer-pyramid`<br>[制度体系四层金字塔自查](../../skills/compliance-assessment/mlps-policy-four-layer-pyramid/SKILL.md) | 方针制度规程记录四层金字塔定位制度体系缺口 | 制度体系分层自查 |
| 合规测评 | `mlps-readiness-self-inspection`<br>[等保就绪度与迎检自查法](../../skills/compliance-assessment/mlps-readiness-self-inspection/SKILL.md) | 按备案常缺项与公安检查口径倒序排查迎检就绪度 | 迎检备案合规准备 |
| 合规测评 | `mlps-separation-of-duties-dual-axis`<br>[职责分离双轴核查](../../skills/compliance-assessment/mlps-separation-of-duties-dual-axis/SKILL.md) | 跨层特权互斥与管理审计角色互斥双轴核查职责闭合 | 职责分离管理核查 |

**来源分布**：Web应用防御×6、体系审核验证×19、合规测评×11

## 覆盖缺口

覆盖较好：体系审核方法论 + 等保测评流程双体系。缺口提示：隐私合规（PIPL/GDPR 细则）、数据出境评估暂无专门技能。
