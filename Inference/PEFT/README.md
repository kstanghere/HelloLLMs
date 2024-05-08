# 快速开始
PEFT微调方式的显著特点是可以只保存更新后的模型权重，而非整个模型模型文件，方便上传与分享
基于此特点，在加载经过PEFT后的模型可以采取如下的方式：
```python
# 设置未经过微调的预训练模型 base_model
base_model = AutoModelForCausalLM.from_pretrained (
    "models/Llama-3-8B-Instruct", device_map = "auto", torch_dtype = torch.bfloat16, trust_remote_code = True
)

# 加载PEFT的模型权重
model_id = "ybelkada/opt-350m-lora"

# 加载微调后的模型
model = PeftModel.from_pretrained(base_model, model_id)

```
Todo list:
- 整理参考其他人是如何加载peft模型的

参考：[Blog 1](https://stackoverflow.com/questions/76459034/how-to-load-a-fine-tuned-peft-lora-model-based-on-llama-with-huggingface-transfo)，[Blog 2](https://stackoverflow.com/questions/76372007/trying-to-install-guanaco-pip-install-guanaco-for-a-text-classification-model/76372390#76372390)

- 整理PeftModel和AutoPeftModel的区别

简而言之，后者可以自动识别base_model是哪个，然后自己去引入，不需要手动配置，而PeftModel需要手动配置，PeftModel适合在base和ft模型的权重都在本地保存时，引入路径，而AutoPeftModel适合已经推送到hub上，参考：[Blog 1](https://blog.csdn.net/aqwca/article/details/134155426), [Blog 2](https://huggingface.co/docs/peft/package_reference/peft_model)，[PEFT docs](https://huggingface.co/docs/peft/v0.10.0/en/package_reference/peft_model)，[PEFT repo](https://github.com/huggingface/peft/tree/v0.10.0)，[Transformers docs](https://huggingface.co/docs/transformers/v4.39.0/en/llm_tutorial)

- 整理LLM生成回答的陷阱，包括为什么推理的时候要采用左填充

参考：[Blog 1](https://huggingface.co/docs/transformers/v4.36.1/zh/llm_tutorial)，[Blog 2 (注意评论区的第一条回答) ](https://zhuanlan.zhihu.com/p/646852375)，[Blog 3](https://zhuanlan.zhihu.com/p/675273498)， [Blog 3](https://github.com/THUDM/ChatGLM2-6B/issues/113)， 

- 整理Chat_Template

参考：[Blog 1](https://huggingface.co/docs/transformers/main/zh/chat_templating), [Blog 2](https://discuss.huggingface.co/t/issue-with-llama-2-chat-template-and-out-of-date-documentation/61645/3), [Repo 1](https://github.com/chujiezheng/chat_templates?tab=readme-ov-file), [Blog 3 Understanding the LLM for Chat Templates](https://claude.ai/chat/8b2d328c-e5d0-4433-af15-6ad731700428)，[Blog 4](https://huggingface.co/spaces/huggingface-projects/llama-2-7b-chat)，[Blog 5](https://huggingface.co/meta-llama/Llama-2-7b-hf/tree/main)