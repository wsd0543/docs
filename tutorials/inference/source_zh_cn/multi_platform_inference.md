# 推理模型总览

 `Linux` `Ascend` `GPU` `CPU` `推理应用` `初级` `中级` `高级`

<!-- TOC -->

- [推理模型总览](#推理模型总览)
    - [模型文件](#模型文件)
    - [执行推理](#执行推理)

<!-- /TOC -->

<a href="https://gitee.com/mindspore/docs/blob/master/tutorials/inference/source_zh_cn/multi_platform_inference.md" target="_blank"><img src="./_static/logo_source.png"></a>

MindSpore可以基于训练好的模型，在不同的硬件平台上执行推理任务。

## 模型文件

MindSpore支持保存两种类型的数据：训练参数和网络模型（模型中包含参数信息）。

- 训练参数指的是Checkpoint格式文件。
- 网络模型包括MindIR、AIR和ONNX三种格式文件。

下面介绍一下这几种格式的基本概念及其应用场景。

- Checkpoint
    - 采用了Protocol Buffers格式，存储了网络中所有的参数值。
    - 一般用于训练任务中断后恢复训练，或训练后的微调（Fine Tune）任务。
- MindIR
    - 全称MindSpore IR，是MindSpore的一种基于图表示的函数式IR，定义了可扩展的图结构以及算子的IR表示。
    - 它消除了不同后端的模型差异，一般用于跨硬件平台执行推理任务。
- ONNX
    - 全称Open Neural Network Exchange，是一种针对机器学习模型的通用表达。
    - 一般用于不同框架间的模型迁移或在推理引擎([TensorRT](https://docs.nvidia.com/deeplearning/tensorrt/api/python_api/index.html))上使用。
- AIR
    - 全称Ascend Intermediate Representation，是华为定义的针对机器学习所设计的开放式文件格式。
    - 它能更好地适应华为AI处理器，一般用于Ascend 310上执行推理任务。

## 执行推理

按照使用环境的不同，推理可以分为以下两种方式。

1. 本机推理

    通过加载网络训练产生的Checkpoint文件，调用`model.predict`接口进行推理验证，具体操作可查看[使用Checkpoint格式文件执行推理](https://www.mindspore.cn/tutorial/inference/zh-CN/master/multi_platform_inference_ascend_910.html#checkpoint)。

2. 跨平台推理

    使用网络定义和Checkpoint文件，调用`export`接口导出模型文件，在不同平台执行推理，目前支持导出MindIR、ONNX和AIR（仅支持Ascend AI处理器）模型，具体操作可查看[保存模型](https://www.mindspore.cn/tutorial/training/zh-CN/master/use/save_model.html)。

MindSpore通过统一IR定义了网络的逻辑结构和算子的属性，将MindIR格式的模型文件与硬件平台解耦，实现一次训练多次部署。需先使用网络定义和Checkpoint文件导出MindIR模型文件，再根据不同需求执行推理任务，如[在Ascend 310上执行推理任务](https://www.mindspore.cn/tutorial/inference/zh-CN/master/multi_platform_inference_ascend_310_mindir.html)、[基于MindSpore Serving部署推理服务](https://www.mindspore.cn/tutorial/inference/zh-CN/master/serving_example.html)、[端侧推理](https://www.mindspore.cn/lite/docs?master)。
