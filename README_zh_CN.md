软件简介
GPT4All 是基于 LLaMa 的～800k GPT-3.5-Turbo Generations 训练出来的助手式大型语言模型，这个模型接受了大量干净的助手数据的训练，包括代码、故事和对话，可作为 GPT4 的平替。
![gpt4all-lora-demo](https://user-images.githubusercontent.com/13879686/228352356-de66ca7a-df70-474e-b929-2e3656165051.gif)
在 M1 Mac 上运行的示例：



自己试试
从  Direct Link or [Torrent-Magnet] 下载 gpt4all-lora-quantized.bin 文件。
克隆此仓库，导航至 chat ，并将下载的文件放在那里。
为操作系统运行适当的命令：
M1 Mac/OSX: cd chat;./gpt4all-lora-quantized-OSX-m1
Linux: cd chat;./gpt4all-lora-quantized-linux-x86
Windows (PowerShell): cd chat;./gpt4all-lora-quantized-win64.exe
Intel Mac/OSX: cd chat;./gpt4all-lora-quantized-OSX-intel
注意：GPU 上的完整模型（需要 16GB 显存）在定性评估中表现更好。

Python 客户端
CPU 接口
要使用带有 CPU 接口的 python 客户端运行，首先使用安装 nomic 客户端 ，然后可以使用以下脚本与 GPT4All 进行交互：pip install nomic

from nomic.gpt4all import GPT4All
m = GPT4All()
m.open()
m.prompt('write me a story about a lonely computer')
显卡接口
有两种方法可以在 GPU 上启动和运行此模型。此处的设置比 CPU 模型稍微复杂一些。

克隆 nomic 客户端 repo 并在主目录中运行 pip install .[GPT4All] 。
运行 pip install nomic 并从此处构建的 wheels 安装额外的 deps
完成后，可以使用如下脚本在 GPU 上运行模型：

from nomic.gpt4all import GPT4AllGPU
m = GPT4AllGPU(LLAMA_PATH)
config = {'num_beams': 2,
          'min_new_tokens': 10,
          'max_length': 100,
          'repetition_penalty': 2.0}
out = m.generate('write me a story about a lonely computer', config)
print(out)
其中 LLAMA_PATH 是 Huggingface Automodel 兼容的 LLAMA 模型的路径，Nomic 目前无法分发此文件。

可以在配置中传递任何 huggingface 生成配置参数。

路线图
短期
（进行中）基于 GPTJ 训练 GPT4All 模型以缓解 llama 分布问题。
（进行中）为此模型创建改进的 CPU 和 GPU 接口。
（未开始）集成 llama.cpp 绑定
（未开始）为模型创建一个良好的对话聊天界面。
（未开始）允许用户选择加入并提交他们的聊天记录以进行后续培训
中期
（未开始）将 GPT4All 与 Atlas 集成以允许文档检索。
被基于 GPTJ 的 GPT4All 屏蔽
（未开始）将 GPT4All 与 Langchain 集成。
（进行中）构建简单的自定义训练脚本以允许用户微调模型。
长期
（未开始）允许任何人使用 Atlas 为后续 GPT4All 版本整理训练数据。
（进行中）使 AI 民主化。
再现性
训练有素的 LoRa 权重：

gpt4all-lora（四个完整的训练阶段）： https ://huggingface.co/nomic-ai/gpt4all-lora
gpt4all-lora-epoch-2（三个完整的训练阶段）https://huggingface.co/nomic-ai/gpt4all-lora-epoch-2
原始数据：

没有 P3 的训练数据
资源管理器：https://atlas.nomic.ai/map/gpt4all_data_clean_without_p3
P3 的完整数据集
资源管理器：https ://atlas.nomic.ai/map/gpt4all_data_clean
