---
name: create-221g-documents
description: 复用本项目现有的 XeLaTeX 模板，填写和修改用于美签的行程单（Itinerary）、个人简历（Resume）、航班住宿安排（Booking），统一调整样式并编译 PDF。用于用户提供个人资料、旅行计划或要求套用这些模板生成签证材料的场景。
---

# 利用 LaTeX 模板填写签证材料

## 唯一目标

直接复制并填写本项目模板，保留现有 A4、黑白、紧凑的排版，生成申请 US 签证时 221(g) 要求补充的材料。

- 禁止重新设计文档、另起一套 LaTeX 工程，或改用 HTML/Word 重建。
- 禁止把 SKILL 根目录当作当前工作目录。
- 禁止虚构任何个人资料和旅行安排。

> [!warning]
>
> 普通文字中的 `&`、`%`、`$`、`#`、`_` 分别转义为 `\&`、`\%`、`\$`、`\#`、`\_`；字面花括号用 `\{`、`\}`，反斜杠用 `\textbackslash{}`。不要转义已有的 LaTeX 命令。

> [!danger]
>
> 故意虚假陈述重要事实或欺诈，可能导致永久签证不适格。因此所有 `info.tex` 里面的信息都不能伪造、虚构、模拟和臆测。

> [!note]
>
> Latex 环境下载地址：
>
> - macOS：https://tug.org/mactex/mactex-download.html
> - Linux：https://tug.org/texlive/quickinstall.html
> - Windows：https://tug.org/texlive/acquire-netinstall.html

## 文件地图

| 文件 | 职责 | 何时读写 |
| --- | --- | --- |
| [references/style.tex](references/style.tex) | 三份材料的公共视觉规范，确保材料风格一致：参数集中在前半部分，实现集中在后半部分 | 首次了解模板或修改任何全局样式时 |
| [references/itinerary/info.tex](references/itinerary/info.tex) | 个人信息、旅行摘要、逐日安排、备注 | 读写行程单时 |
| [references/itinerary/itinerary.tex](references/itinerary/itinerary.tex) | 行程单 | 读写行程单时 |
| [references/resume/info.tex](references/resume/info.tex) | 个人信息、教育经历、出国经历、实习经历、其它信息 | 读写简历时 |
| [references/resume/resume.tex](references/resume/resume.tex) | 个人简历 | 读写简历时 |
| [references/booking/info.tex](references/booking/info.tex) | 个人信息、航班信息、住宿信息、备注 | 读写机酒清单时 |
| [references/booking/booking.tex](references/booking/booking.tex) | 机酒清单 | 读写机酒清单时 |

## info.tex

### Itinerary

| 宏 | 宏含义 |
| --- | --- |
| `\visaCategory{签证类型}` | 签证类型，显示在文档副标题中 |
| `\personalrow{字段名}{字段值}` | 个人信息，按顺序每两个字段一行，字段名自动转为大写 |
| `\personalwide{字段名}{字段值}` | 独占一行的个人信息，适合住址等长内容 |
| `\entryDate{...}` | 入境日期 |
| `\exitDate{...}` | 离境日期 |
| `\tripDuration{...}` | 行程天数，必须核对与入境至离境的日期一致 |
| `\destinations{...}` | 旅行城市，必须按实际顺序列出 |
| `\arrivalFlight{...}` | 入境航班 |
| `\arrivalCity{...}` | 入境城市 |
| `\departureFlight{...}` | 离境航班 |
| `\departureCity{...}` | 离境城市 |
| `\travelParty{...}` | 同行人 |
| `\budget{...}` | 预算，单位必须是前往国家的币种 |
| `\dayrow{日期}{地点}{安排}{住宿}{交通}` | 一天行程，活动保持简洁，以动名词短语或旅游景点为主 |
| `\noterow{备注}` | 一条备注，只包含必要提示信息 |

### Resume

| 宏 | 宏含义 |
| --- | --- |
| `\visaCategory{签证类型}` | 签证类型，显示在文档副标题中 |
| `\personalrow{字段名}{字段值}` | 个人信息，按顺序每两个字段一行，字段名自动转为大写 |
| `\personalwide{字段名}{字段值}` | 独占一行的个人信息，适合住址等长内容 |
| `\educationentry{学校}{学位}{起止}` | 一段教育经历，学位包含专业，起止注明年月 |
| `\travelentry{国家或地区}{目的}{起止}` | 一次出国或出境经历，目的通常为旅游或研学，起止注明年月日 |
| `\internshipentry{公司}{职位}{起止}{概述}{职责}` | 一段实习经历，概述内容可留空 `{}`，职责参数中填写 `\duty{...}` |
| `\otherentry{字段名}{字段值}` | 语言、技能、兴趣、发表等补充信息，字段值为空时整条不显示 |

### Booking

| 宏 | 宏含义 |
| --- | --- |
| `\visaCategory{签证类型}` | 签证类型，显示在文档副标题中 |
| `\personalrow{字段名}{字段值}` | 个人信息，按顺序每两个字段一行，字段名自动转为大写 |
| `\personalwide{字段名}{字段值}` | 独占一行的个人信息，适合住址等长内容 |
| `\flightrow{航班号}{出发机场}{出发城市}{出发时间}{到达机场}{到达城市}{到达时间}` | 一段航班，机场填写代码，时间使用当地时间，核对跨时区和跨日到达 |
| `\accommodationrow{城市}{入住日期}{退房日期}{住宿名称}{联系方式}{地址}{邮编}` | 一段住宿，核对入住和退房日期与行程一致，地址可用 `\newline` 分行 |
| `\noterow{备注}` | 一条备注，只包含必要提示信息 |

## 工作流程

1. 根据用户输入，确认需要哪几份材料，读取 `style.tex`、相应主文件和相应 `info.tex`。
2. 提取用户已提供的信息和资料，只追问影响交付的缺失事实和 `info.tex` 尚未补充的真实信息。
3. 复制 `references/` 下的公共模板到私有工作目录后，在私有副本的 `info.tex` 中填写数据，必须核对：
    - 多份材料之间的数据一致对齐
    - 没有违背客观事实的非法字段值
    - 没有漏改示例字段
    - 没有任何假数据
4. 若缺失  XeLaTeX 环境则下载安装，在私有副本的各文档子目录中使用 XeLaTeX 编译，判断命令成功退出和 PDF 确实生成，必须检查
    - 日志没有报错，若有则按具体错误内容修复
    - PDF 页面没有出现内容截断、表格越界、空白页、孤立标题、阅读字号、字符乱码等问题
    - PDF 不是历史过期文件，必须是基于最新的 `.tex` 文件生成。
5. 交付 PDF 和 `info.tex` 给用户审查。
