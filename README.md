# Deep Water

UPC OJ 日常练习脚本。用 DeepSeek 生成 C++17 题解，根据判题结果修正，按北京时间统计每天首次通过的题数。

## 快速开始

需要 `uv` 和 Python 3.13 或更新版本。在项目目录运行：

```sh
uv sync
cp -n .env.example .env
```

按下表填写 `.env`，再运行 `uv run main.py`。默认是只读预览：登录 OJ、核对当天记录并显示候选题，不调用 DeepSeek，也不提交。

| 环境变量 | 用途 | 默认值 |
| --- | --- | --- |
| `OJ_USER` | UPC OJ 账号 | 必填 |
| `OJ_PASSWORD` | UPC OJ 原始密码 | 必填 |
| `DEEPSEEK_API_KEY` | DeepSeek API Key | 提交模式必填 |
| `DEEPSEEK_MODEL` | DeepSeek 模型 | `deepseek-flash` |
| `DAILY_TARGET` | 每天首次通过的目标题数 | `1` |
| `OJ_SUBMIT_INTERVAL_SECONDS` | 两次提交的最小间隔，单位为秒 | `5` |

系统环境变量优先于 `.env`。不要分享 `.env`。

Windows 上如果看到 `ZoneInfoNotFoundError: 'No time zone found with key Asia/Shanghai'`，在项目目录运行 `uv sync`，再用 `uv run main.py` 启动。若直接用 Conda 的 Python 运行，请在同一环境里执行 `python -m pip install tzdata`。

## 运行模式

请先确认站方允许自动化和 AI 提交，仅用于非比赛练习。

```sh
uv run main.py                 # 预览
uv run main.py --submit        # 补足当天目标后退出
uv run main.py --submit --loop # 保持进程运行，北京时间跨日后再检查
```

已经通过的题不会重复选。脚本优先复用 `.oj-cache/` 中的可读题面，候选不足时继续逐页扫描。题面和判题结果用于 DeepSeek 的多轮解题；模型可以主动换题，每题最多提交 10 次。若扫完整个题库仍未达标，脚本会报告实际题数。遇到验证码、提交异常或判题结果不明时停止，不盲目重发。

## 鲸鱼娘火车头

每次提交从六张同画风的 Q 版鲸鱼娘里随机抽一张，以 42 行 ASCII 注释放在 C++ 源码开头。表情预存于 `fish_headers.py`，运行时无需下载；原图来自 [1cyberlangke1 的小鲸鱼表情包](https://github.com/lmy414/ai-girl-stickers/issues/32)（投稿标注 CC0）。
