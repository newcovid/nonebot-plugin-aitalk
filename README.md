<div align="center">
  <a href="https://v2.nonebot.dev/store"><img src="https://github.com/A-kirami/nonebot-plugin-template/blob/resources/nbp_logo.png" width="180" height="180" alt="NoneBotPluginLogo"></a>
  <img src="https://github.com/WStudioGroup/hifumi-plugins/blob/main/remove.photos-removed-background.png" width="200">
  <br>
  <p><img src="https://github.com/A-kirami/nonebot-plugin-template/blob/resources/NoneBotPlugin.svg" width="240" alt="NoneBotPluginText"></p>
</div>

<div align="center">

# nonebot-plugin-aitalk

_✨ 简单好用的 AI 聊天插件 ✨_

<a href="./LICENSE">
    <img src="https://img.shields.io/github/license/captain-wangrun-cn/nonebot-plugin-aitalk.svg" alt="license">
</a>
<a href="https://pypi.python.org/pypi/nonebot-plugin-aitalk">
    <img src="https://img.shields.io/pypi/v/nonebot-plugin-aitalk.svg" alt="pypi">
</a>
<img src="https://img.shields.io/badge/python-3.9+-blue.svg" alt="python">

</div>

## 📖 介绍

简单好用的 AI 聊天插件，支持多 API，支持让 AI 理解图片，发送表情包，合成语音，艾特，禁言/解除禁言，戳一戳等；可配置关键词允许 AI 主动发言

> [!IMPORTANT]
> 写的比较史，欢迎提 pr 或 issue！

欢迎查看我的另一个独立框架，支持持久记忆，高度自定义，主动消息以及创新架构：https://github.com/captain-wangrun-cn/N.O.R.A.Core

## 🆕 特色

### AI 可以发的

- 表情包
- 语音（非预设语录，AI 想说什么就生成什么）
- 戳一戳
- 艾特
- 群内禁言

### 可以发给 AI 的 (AI 可以理解的)

- 图片/表情包 (需模型支持)
<!--- 联网搜索 (需模型支持)-->

## 💿 安装

<details open>
<summary>使用 nb-cli 安装</summary>
在 nonebot2 项目的根目录下打开命令行, 输入以下指令即可安装

    nb plugin install nonebot-plugin-aitalk

</details>

<details>
<summary>使用包管理器安装</summary>
在 nonebot2 项目的插件目录下, 打开命令行, 根据你使用的包管理器, 输入相应的安装命令

<details>
<summary>pip</summary>

    pip install nonebot-plugin-aitalk

</details>

打开 nonebot2 项目根目录下的 `pyproject.toml` 文件, 在 `[tool.nonebot]` 部分追加写入

    plugins = ["nonebot_plugin_aitalk"]

</details>

## ⚙️ 配置

在 nonebot2 项目的`.env`文件中添加下表中的必填配置

### 必填项

|         配置项         | 类型 | 必填 | 默认值 |                 说明                 |
| :--------------------: | :--: | :--: | :----: | :----------------------------------: |
|    aitalk_api_list     | list |  是  |  [ ]   | API 列表，支持多个 API，格式请往下看 |
| aitalk_available_memes | list |  是  |  [ ]   |   AI 可以发送的表情包，格式请往下    |

<details>
<summary>aitalk_api_list（api列表）格式</summary>
  
```json
[
{
    "name": "向用户展示的模型名称",
    "api_key": "你的api key",
    "model_name": "请求api用的模型名称",
    "api_url": "api接口地址",
    "image_input": 是否支持图片输入，适用于Qwen2.5-vl等多模态模型,默认为false
    "send_thinking": 当有思维链时是否发送,默认为false
    "description": "模型描述，用于展示给用户(非必填)"
},
{
    "name": "向用户展示的模型名称2",
    "api_key": "你的api key2",
    "model_name": "请求api用的模型名称2",
    "api_url": "api接口地址2"
}
]
```

</details>

<details>
<summary>aitalk_available_memes（AI可以发送的表情包）格式</summary>

```json
[
  {
    "url": "图片地址，支持链接或本地路径。⚠️⚠️注意！如果是windows系统的本地路径，请将路径中的换成/，可以看下面的配置示例⚠️⚠️",
    "desc": "图片描述，告诉AI这张表情包是什么内容，用于什么场景等等"
  },
  {
    "url": "图片地址2",
    "desc": "图片描述2"
  }
]
```

</details>

### 选填项

#### 模型

|        配置项        | 类型 | 必填 | 默认值 |      说明      |
| :------------------: | :--: | :--: | :----: | :------------: |
| aitalk_default_model | str  |  否  |   ""   | 默认选择的模型 |

#### 提示词

|           配置项            | 类型 | 必填 |                                            默认值                                            |                                                                   说明                                                                    |
| :-------------------------: | :--: | :--: | :------------------------------------------------------------------------------------------: | :---------------------------------------------------------------------------------------------------------------------------------------: |
|    aitalk_default_prompt    | str  |  否  | "你的回答应该尽量简洁、幽默、可以使用一些语气词、颜文字。你应该拒绝回答任何政治相关的问题。" |                                                                默认提示词                                                                 |
| aitalk_disable_busy_prompts | bool |  否  |                                            False                                             |                                     是否关闭诸如“不要着急哦！”或“你的操作太频繁了哦！”之类的提示信息                                      |
| aitalk_default_prompt_file  | str  |  否  |                                              ""                                              |                         默认提示词文件路径，与提示词二选一，优先使用文件。请注意将 windows 系统路径中的\替换成\\                          |
|  aitalk_group_prompts_dir   | str  |  否  |                               "./aitalk_config/group_prompts"                                | 分群提示词文件路径，在该路径下存放"群号.txt"文件，(例如: ./aitalk_config/group_prompts/12345.txt)。请注意将 windows 系统路径中的\替换成\\ |

#### 语音合成

|       配置项       | 类型 | 必填 | 默认值 |            说明            |
| :----------------: | :--: | :--: | :----: | :------------------------: |
| aitalk_tts_enabled | bool |  否  | false  |      是否开启语音合成      |
| aitalk_tts_config  | bool |  否  | false  | 语音合成配置，详细请看下方 |

<details>
<summary>aitalk_tts_config（语音合成配置）格式</summary>
  
```json
{
    "api_url": "API地址，若默认地址无法访问可以自己搭建一个反向代理",
    "api_key": "API密钥",
    "reference_id": "音色id"
}
```
- 前往[FishAudio](https://fish.audio/zh-CN/go-api/billing/)注册登录，并充值（建议先一美元）
- 创建一个API key并填入配置项![api_key](imgs/QQ20250507-133925.png)
- 点击上面的`发现`，寻找你想要的音色（或者有能力的自己合成），点进去
- 复制图片中地址的红圈部分，该部分就是id，填入配置即可![id](imgs/QQ20250507-134145.png)

</details>

#### 消息相关

|                   配置项                    | 类型  | 必填 | 默认值 |                                               说明                                                |
| :-----------------------------------------: | :---: | :--: | :----: | :-----------------------------------------------------------------------------------------------: |
|           aitalk_reply_when_meme            | bool  |  否  |  true  |                                   当只有表情包时，是否回复消息                                    |
|                aitalk_reply                 | bool  |  否  |  true  |                                           是否回复消息                                            |
|        aitalk_message_send_delay_min        | float |  否  |  0.2   |                     发送多条消息时，每条之间的最小延迟（秒），设为 0 则不延迟                     |
|        aitalk_message_send_delay_max        | float |  否  |  1.2   |                     发送多条消息时，每条之间的最大延迟（秒），设为 0 则不延迟                     |
|     aitalk_active_reply_context_timeout     |  int  |  否  |  300   |                             机器人主动回复后，上下文的有效时间（秒）                              |
| aitalk_active_reply_max_unrelated_followups |  int  |  否  |   3    | 在主动回复上下文中，AI 连续判断 N 次与追问无关后，关闭本次主动回复会话 (0 表示不启用此功能)（秒） |
|      aitalk_group_active_reply_configs      | Dict  |  否  |   {}   |             分群独立主动回复配置。键为群号字符串，值为该群的特定配置,详见下方配置示例             |
|         aitalk_active_reply_enabled         | bool  |  否  | False  |                                       是否启用主动回复功能                                        |

#### 其他

|                   配置项                   |   类型    | 必填 | 默认值 |                                         说明                                         |
| :----------------------------------------: | :-------: | :--: | :----: | :----------------------------------------------------------------------------------: |
|            aitalk_command_start            |    str    |  否  |   ""   |          对话触发前缀，例如“/对话”，类似 on_command，为空时直接艾特即可触发          |
|          aitalk_completion_config          |   list    |  否  |  [ ]   |                                生成配置，格式请往下看                                |
|          aitalk_max_split_length           |    int    |  否  |   5    |  最大分割长度，将会在 prompt 中告诉 ai，回复的消息数量不要大于这个值，可能不起作用   |
|         aitalk_max_context_length          |    int    |  否  |   20   | 最长上下文消息数量，超过这个数量时，将会逐个抛弃最早的一条消息。这个数值包括设定消息 |
|          aitalk_save_user_config           |   bool    |  否  |  true  |    是否保存用户配置，关闭 nonebot 时将会保存用户所选模型，对话内容等，启动时读取     |
|          aitalk_default_available          |   bool    |  否  |  true  |                是否默认允许群聊使用，为 false 时需要手动使用指令开启                 |
|      aitalk_default_available_private      |   bool    |  否  |  true  |                是否默认允许私聊使用，为 false 时需要手动使用指令开启                 |
|               aitalk_chat_cd               |    int    |  否  |   5    |                                   聊天 cd，单位秒                                    |
|        aitalk_active_reply_keywords        | list[str] |  否  |   []   |              主动回复的触发关键字列表, 例如 '["问题", "请问", "大佬"]'               |
|      aitalk_active_reply_probability       |   float   |  否  |  0.3   |                    满足关键字后，触发主动回复的概率 (0.0 到 1.0)                     |
| aitalk_active_reply_no_keyword_probability |   float   |  否  |  0.05  |          未满足关键字时，触发主动回复的概率 (0.0 到 1.0)，建议设置较低的值           |
|                aitalk_proxy                |    str    |  否  |  None  |                     为模型使用的代理,例如"http://127.0.0.1:7897"                     |

<details>
<summary>aitalk_completion_config（生成配置）格式</summary>

```json
{
    "max_token": 1024,
    "temperature": 0.7
    "top_p": 0.9
}
```

</details>

## ⚙️ 配置示例

<details>
<summary>env配置示例</summary>

```
aitalk_default_model = "deepseekr1"
aitalk_api_list = '
[
{
    "name": "deepseekr1",
    "api_key": "sk-1145141919810",
    "model_name": "deepseek-ai/DeepSeek-R1",
    "api_url": "https://api.siliconflow.cn/v1",
    "send_thinking": true
},
{
    "name": "gemma-27b",
    "api_key": "sk-1145141919810",
    "model_name": "google/gemma-2-27b-it",
    "api_url": "https://api.siliconflow.cn/v1"
}
]
'
aitalk_available_memes = '
[
{
    "url": "D:/bots/imgs/1.png",
    "desc": "很抱歉伤害到你"
},
{
    "url": "D:/bots/imgs/3.png",
    "desc": "啊哈哈...（感到尴尬）"
}
]
'

aitalk_default_prompt_file = "D:\\prompt\\日富美.txt"
aitalk_group_prompts_dir = "./aitalk_config/group_prompts"

aitalk_tts_enabled = true
aitalk_tts_config = '
{
    "api_url": "https://api.fish.audio",
    "api_key": "114514919810",
    "reference_id": "fee77b5adcb840178e9596514d713a3b"
}
'

aitalk_message_send_delay_min = 0.3
aitalk_message_send_delay_max = 1.2

aitalk_active_reply_enabled = true
aitalk_active_reply_keywords = '["问题","请问","大佬","咋弄","咋搞","怎么","解压密码"]'
aitalk_active_reply_probability = 1.0
aitalk_active_reply_no_keyword_probability = 0.05
aitalk_group_active_reply_configs = '
{
    "123456": {
        "keywords": ["临时触发词temp"],
        "probability": 1.0,
        "no_keyword_probability": 0.05
    },
    "654321": {
        "keywords": ["问题","请问","大佬","咋弄","咋搞","怎么"],
        "probability": 1.0,
        "no_keyword_probability": 0.05
    }
}'

aitalk_disable_busy_prompts = Ture
```

#### 多群自定义提示词参考配置

<img src="imgs/Snipaste_2025-05-06_23-17-39.png">

</details>

## 🎉 使用

### 指令表

|     指令     |  权限   | 需要@ | 范围 |        说明        |
| :----------: | :-----: | :---: | :--: | :----------------: |
|   @机器人    |  群聊   |  是   | 群聊 | 艾特机器人即可聊天 |
|   模型选择   |  群聊   |  否   | 群聊 |      选择模型      |
| ai 对话 开启 | 管理员+ |  否   | 群聊 |  开启本群 ai 对话  |
| ai 对话 关闭 | 管理员+ |  否   | 群聊 |  关闭本群 ai 对话  |
| 清空聊天记录 |  群聊   |  否   | 群聊 |    清空对话记录    |

### 效果图

<img src="imgs/QQ20250222-232704.png">
<img src="imgs/QQ20250222-232730.png">
<img src="imgs/QQ20250222-232813.png">
<img src="imgs/QQ20250507-134732.png">
她不肯说qwq
<img src="imgs/qq_pic_merged_1761231455574.jpg">

### 🍟 参考

[nonebot-plugin-llmchat](https://github.com/FuQuan233/nonebot-plugin-llmchat) 参考了部分代码以及 prompt

## 贡献者

<a href="https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=captain-wangrun-cn/nonebot-plugin-aitalk" />
</a>

## 📃 更新日志

### 3.13.38（2026.01.01）

- 🐛 修复了依赖fish_audio_sdk版本问题

### 3.13.37（2025.11.01）

- 🔧 群内聊天时使用群昵称

### 3.13.36（2025.10.28）

- 🐛 尝试修复无法获取消息中艾特的问题

### 3.13.34（2025.10.28）

- 🐛 修复 bot 是群主时的禁言/解禁问题[#23](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/23)
- 🆕 允许自定义关闭禁言/解禁失败提示

### 3.13.33（2025.10.27）

- 🆕 允许自定义模型的代理[#22](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/22)

### 3.12.33（2025.10.23）

- 🆕 添加解除禁言功能[#21](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/21)

### 3.11.28（2025.05.25）

- 🆕 新增默认模型配置项

<details>
<summary>之前更新</summary>

### 3.11.33（2025.08.15）

- 🐛 移除无用依赖

### 3.11.32（2025.06.17）

- 🐛 修复了语音配置报错问题

### 3.11.31（2025.06.11）

- 🐛 修复了起始符配置项不生效的问题[#20](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/20)

### 3.11.30（2025.06.10）

- 🐛 删除无用依赖
- 🐛 修复某些 API 下的多模态模型出现 Error Code 400[#19](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/19)

### 3.11.29（2025.06.10）

- 🐛 修复某些 API 下的多模态模型出现 Error Code 400[#19](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/19)

### 3.10.28（2025.05.21）

- 🐛 修复“无需回复”BUG[PR#16](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/16)
- 🆕 允许关闭提示[PR#16](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/16)
- 🐛 修复某些情况下 QQ 图片因 SSL 无法下载的问题

### 3.9.26（2025.05.12）

- 🆕 更新多群配置主动触发关键词
- 🔧 增加对 AI 返回的 JSON 字符串的解析的鲁棒性
- [PR#15](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/15)

### 3.8.25（2025.05.11）

- 🆕 支持读取引用消息中的文本
- 🆕 增加配置，允许 AI 在回复多条消息时增加随机延迟
- 🆕 增加配置，允许在检测到关键词时询问 AI，由 AI 自主决定是否需要主动发言回复用户。
- 🆕 增加独立的 JSON 修复功能，用于在主聊天 AI 返回的 JSON 格式错误后，尝试使用独立对话 AI 自动修复该 JSON 格式。
- 🔧 更新 README.md 中的配置项
- [PR#14](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/14)

### 3.4.24（2025.05.08）

- 🐛 修复戳一戳失败的问题[PR#13](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/13)

### 3.5.23（2025.05.07）

- 🆕 图片输入支持引用带有图片的消息[PR#12](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/12)
- 🆕 支持多图输入[PR#12](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/12)
- 🔧 添加了一些请求时的异常处理
- 🐛 修复 README 中配置不完全

### 3.4.22（2025.05.07）

- 🆕 新增语音合成功能
- 🔧 优化 README

### 2.4.21（2025.05.07）

- 🆕 新增分群不同提示词功能
- 🐛 其他中量代码优化[PR#11]
- (https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/11)

### 2.3.20（2025.04.01）

- 🐛 尝试修复思维链问题(#10)(https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/10)
- 🆕 添加了模型描述，选择模型时发送给用户

### 2.3.19（2025.03.11）

- 🐛 修复 Q 群管家检测 BUG

### 2.3.18（2025.03.07）

- 🐛 修复思维链输出

### 2.3.17（2025.03.07）

- 🐛 修复超出最长上下文数量时的 BUG
- 🆕 增加禁言用户的功能[PR#8](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/8)

### 2.2.16（2025.03.06）

- 🐛 修复私聊开关 BUG

### 2.2.15（2025.03.05）

- 🆕 支持输出思维链(不推荐开启，思维可能错乱)
- 🔧 优化 prompt
- 🐛 再次修复读取“是否回复”配置项的 BUG，并测试通过[PR#5](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/5)

### 2.1.14（2025.03.04）

- 🐛 修复生成失败后队列未移除 BUG

### 2.1.13（2025.03.04）

- 🐛 修复路径 BUG 和配置读取 BUG[PR#4](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/pull/4)

### 2.1.12（2025.03.04）

- 🆕 支持让 AI 理解图片（图片输入）
- 🐛 优化代码
- 🆕 更改群聊聊天,支持管理员设置群内模型[#1](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/1)
- 🐛 修复连续对话问题[#2](https://github.com/captain-wangrun-cn/nonebot-plugin-aitalk/issues/2)

### 1.0.10（2025.03.02）

- 🐛 修复了设置输入状态的问题

### 1.0.9（2025.02.28）

- 🐛 修复了私聊聊天的一些问题

### 1.0.8（2025.02.28）

- 🆕 添加了私聊聊天支持

### 1.0.7（2025.02.25）

- 🐛 更改 data.py

### 1.0.6（2025.02.23）

- 😡 排除 Q 群管家

### 1.0.5（2025.02.23）

- 🐛 修复了表情包链接问题

### 1.0.4（2025.02.23）

- 🐛 修复一些问题,更改 README

### 1.0.3（2025.02.23）

- ⬇️ 修复依赖问题

### 1.0.2（2025.02.23）

- 🐛 修复表情包本地路径问题

### 1.0.1（2025.02.22）

- 📝 更新 README

### 1.0.0（2025.02.22）

- 🎉 发布

</details>
