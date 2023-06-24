Fork自https://github.com/alexogeny/cortana，在其基础上继续进行开发

# Cortana - the magic of AI

Cortana is an AI-powered python library for achieving several tasks:

- chatting with GPT via command line
- doing speech to text with openai-whisper
- doing text to speech with elevenlabs
- creating a personal assistant with whisper, GPT, and elevenlabs
- speaking with a different voice using whisper and elevenlabs

Example dialogue (user speaks into microphone, assistant speaks responses back):

```plaintext
System: 你是Cortana，John的40岁的assistant。 你的个性是humorous, sarcastic, sassy，喜欢witty, dry。 你对technology, gadgets, software, artifical intelligence感兴趣。 不要以第三人称自称为AI、助手或机器人。保持对话方式。 尽量避免随机回复非常长的消息。
```

## How it works

Cortana使用whisper进行语音转文本，然后使用GPT生成响应。~~然后使用elevenlabs进行文本转语音~~，然后使用macos里的TTS进行文本转语音，并输出音频。

~~辅助模式具有热词检测系统，因此您可以说出您想要激活助手的热词。然后它会听取命令，然后进行响应。它将忽略不包含热词的任何命令。~~

~~目前它还没有办法检测没有热词的信息是否属于对话。~~

对于中文来说，hotword 识别率太低，当前版本 (v0.1.0) 采用回车键来触发语音输入。

它将在/chats文件夹中记录使用ChatGPT的所有聊天记录。

## Installation

Make sure pipenv is available on your path, then simply:

```bash
# pipenv install
cp example.env .env
```

请在 .env 文件中输入您的 OpenAI API，~~并更改名称和语音。语音应该是[elevenlabs API](https://elevenlabs.io/)提供的语音之一，包括默认语音或您克隆的语音。它将选择第一个匹配的语音（不区分大小写）。~~

~~对于音频设置，我使用了一个虚拟音频混音器。如果您没有混音器，请查看您的音频设备以查看设备名称，并在 .env 文件中进行设置。~~

## Usage

不要在IDE里运行，而是要在macos的默认终端里运行，否则收不到语音输入

```bash
# pipenv shell
python cli.py --help
```

To run the full assistant pipeline:

```bash
python cli.py full
```

## Notes

默认情况下，它将使用gpt-4。如果您没有访问GPT-4的API，则在 .env 文件中将模型更改为gpt-3.5-turbo。

~~此外，它假设您有 elevenlabs 的 API 密钥。如果没有，您可以在 [elevenlabs](https://elevenlabs.io/) 上免费试用一些角色获取一个 API 密钥。~~

如果您发现whisper tiny模型不够准确，请将模型大小提高到small或medium。这样做会影响性能速度，但准确性会更高。我发现“small”模型在没有任何微调的情况下就可以很好地工作。

语音被缓存到voices.json中以节省 API 调用。如果您想刷新语音，请删除该文件。


## Limitations

目前只在 MacOS 上可用，并且暂时没有支持其他平台的计划，因为我只有一台电脑，一个Macbook air m1

## Future goals / todos

做一个可以陪我，给我出主意，帮我执行操作的Cortana
