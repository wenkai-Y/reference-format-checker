# reference-format-checker

一个用于 Claude 的自定义 Skill,检查参考文献格式是否符合**国科大硕士论文要求**(基于 [GB/T 7714—2015](http://www.gb688.cn/bzgk/gb/) 标准),并自动验证英文标点符号后的空格规范。

> 适用于使用 Claude 网页版 / 桌面版的研究生、科研工作者,在写论文前一键检查参考文献列表。

---

## 功能

- ✅ 支持 12 种文献类型:专著 `[M]`、期刊 `[J]`、学位论文 `[D]`、会议论文 `[C]`、报告 `[R]`、专利 `[P]`、标准 `[S]`、报纸 `[N]`、档案 `[A]`、电子资源 `[EB/OL]`、在线图书 `[M/OL]`、在线报告 `[R/OL]`
- ✅ 检查必填字段(责任者、出版地、出版者、出版年、页码等)
- ✅ 检查文献类型标识
- ✅ 检查中文文献是否一致使用半角标点
- ✅ **检查英文文本中标点符号后是否有空格**(常见错误)
- ✅ 检查日期格式 (`YYYY-MM-DD`)
- ✅ 检查 URL 字段
- ✅ 逐条报错 + 汇总统计

## 输入方式

两种使用方式:

1. **粘贴文本** —— 直接在对话里粘贴参考文献列表
2. **指定文件** —— 提供文件路径,支持 `.md` / `.txt` / `.tex` / `.docx`

---

## 安装

### 前置条件

打开 Claude 设置,确认以下两项已开启:

1. **Settings → Capabilities → Code execution and file creation** ✅
2. **Settings → Capabilities → Skills** ✅

### 安装步骤

1. 下载本仓库(`Code → Download ZIP`),或克隆:

   ```bash
   git clone https://github.com/<你的用户名>/reference-format-checker.git
   ```
2. 进入仓库目录,把内层的 `reference-format-checker/` 文件夹**单独压缩成 zip**
   - macOS:右键文件夹 → "压缩"
   - Windows:右键 → "发送到 → 压缩文件夹"
   - 命令行:`cd reference-format-checker && zip -r ../reference-format-checker.zip reference-format-checker`
3. 打开 Claude → **Customize → Skills** → 点击 **"+"** → **"+ Create skill"** → 上传刚才的 zip
4. 在 skill 列表中**打开**这个 skill 的开关

> ⚠️ 注意:zip 内必须直接包含 `SKILL.md` 所在的那个文件夹,不能多套一层。

---

## 使用

安装并启用后,直接对话即可,例如:

```
帮我用 reference-format-checker 检查下面这段参考文献:

[1] 李祥浩. 青藏高原东缘环境与生态[M]. 成都: 四川大学出版社, 2002: 20.
[2] Bravo H,Olavarria J,Torrealba F. Comparative study...[J]. Anat Embryol, 1990,181:67-73.
```

Claude 会逐条检查并返回:

```
[1] ✅ 通过
[2] ❌ 英文逗号后缺少空格:"Bravo H,Olavarria J,Torrealba F"
     ❌ 英文逗号、冒号后缺少空格:"1990,181:67-73"

汇总:共 2 条,通过 1 条,问题 1 条。
```

也可以指定文件:

```
检查 /path/to/references.md 的参考文献格式
```

---

## 仓库结构

```
reference-format-checker/
├── README.md                       本文件
├── LICENSE                         MIT 协议
├── .gitignore
├── reference-format-checker/       ← 这个文件夹是要打包上传的 skill
│   └── SKILL.md                    skill 主文件
└── examples/                       测试样例
    ├── correct.md                  格式正确的参考文献
    └── with-errors.md              含常见错误的参考文献
```

---

## 检查规则概览

详细规则见 [`reference-format-checker/SKILL.md`](./reference-format-checker/SKILL.md)。核心规则:

### 通用格式

```
主要责任者. 题名[文献类型]. 出版地: 出版者, 出版年: 页码.
```

### 英文标点空格规则(易错点)

> 所有英文文本中,英文标点符号后必须有且仅有一个空格(条目末尾的 `.` 除外)。

| 标点 | 正确 | 错误 |
|------|------|------|
| `,` | `Bravo H, Olavarria J` | `Bravo H,Olavarria J` |
| `:` | `Geneva: WHO` | `Geneva:WHO` |
| `.` | `1990, 181: 67-73.` | `1990,181:67-73.` |

### 中文文献标点

中文文献的标点统一使用**半角**(`. , : ;`),不使用全角(`。，：；`),与样例保持一致。

---

## 贡献

发现 bug 或想新增检查规则?欢迎:

- 提 [Issue](../../issues)
- 提 [Pull Request](../../pulls)

可改进方向:
- 增加更多文献类型样例
- 增加 BibTeX 格式输入支持
- 增加自动修正(而不仅是报错)
- 适配其他高校的论文格式规范

---

## 参考标准

- **GB/T 7714—2015** 《信息与文献 参考文献著录规则》
- 中国科学院大学硕士学位论文撰写规范

---

## License

MIT —— 详见 [LICENSE](./LICENSE)。Skill 文件本身基于 GB/T 7714—2015 国家标准编写,标准本身的著作权归属相应机构。
