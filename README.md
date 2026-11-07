# 西安建筑科技大学 - 智建课堂录音助手 (iOS 原生版)

建大专属的智能随堂录音、课表导入与 DeepSeek AI 助教 App（原生 SwiftUI + iOS 15+ 兼容）。

---

## 🌟 核心特性与架构

1. **课表全周网格视图 (Timetable)**：
   - 完整 12 节次时间轴（08:30–20:35）与 7 天列网格，还原教务系统课表视觉风格。
   - 智能识别建大智建专业 PDF，一键导入 17 门课程、64 个节次安排，教室与教师信息准确无误。
   - 顶栏支持 1–20 周自由周次切换，并在日历头部以黑色圆标高亮今日。

2. **转录引擎自由切换 (Dual ASR Engines)**：
   - **苹果原生语音识别 (`SFSpeechRecognizer`)**：使用本地 iOS 语音识别引擎，免配置 Key、完全离线、低延迟实时出字、零流量消耗。
   - **阶跃星辰 ASR (`stepaudio-2.5-asr`)**：基于阶跃云端高精模型，深度识别学术公式、定理人名与专业生僻词。
   - 在录音首页与设置页均提供一键切换开关。

3. **AI 助教问答与 Markdown 结构化笔记**：
   - 接入 **DeepSeek v4.1 Flash** (`deepseek-v4.1-flash-1017`)，专注解答公式推导、考点梳理与课堂解惑。
   - 支持多段实录多选、单段长按追问。
   - **NativeTableView 原生表格对齐引擎**：统一度量各列宽度，表头与数据行垂直贯通，杜绝 Markdown 表格错位。

4. **存储空间极致释放 (Zero Audio Residue)**：
   - 录音转录与纪要生成后，底层自动删除 `.caf` 原始大音频文件，每节课仅占用几 KB 的 JSON 存储，彻底告别手机空间不足。
   - 播放控制栏自适应展示归档提示。

5. **实录文字“多选复制”**：
   - 支持进入多选模式、一键全选或自由勾选多段文字。
   - 底部浮动栏一键按时间戳合并复制至剪贴板，方便粘贴到备忘录。

---

## 🔄 Git 版本回退与历史记录指南

本项目已严格按照语义化版本打标，随时支持一键回退到任一历史版本：

```bash
# 查看所有历史提交与说明
git log --oneline --graph

# 查看所有发布的版本标签
git tag -l

# 回退/切换到指定版本查看：
git checkout v1.2.0   # 当前最新稳定版（表格对齐、ASR切换、PDF导入优化、多选复制）
git checkout v1.1.0   # 集成 DeepSeek 问答与阶跃 ASR 版
git checkout v1.0.0   # 最初版原生应用

# 如需将代码强行重置到某一版本：
git reset --hard v1.2.0
```

---

## 🚀 编译与自动化打包 (CI/CD)

项目配置了 GitHub Actions 自动化构建工作流：
- 配置文件：`.github/workflows/build-ios.yml`
- 运行环境：`macos-15` (Xcode 16.2)
- 产物构建：自动编译为 64 位 ARM64 Mach-O 原生二进制，并使用 Ad-Hoc 证书免越狱打包为 `.ipa`。
- 本地监控与下载脚本：`python scripts/monitor_and_download_ipa.py`

产物路径：`D:\IOS\建大课堂录音.ipa`
安装方式：支持使用 **Sideloadly**、**Feather** 或 **AltStore** 直接侧载安装到 iPhone。
