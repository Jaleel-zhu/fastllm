## V0.0.0.8

- api server增加api_key参数，来设定api_key
- api server支持了一些复合输入
- 提升了moe模型prefill的速度
- 隐藏了 "None of PyTorch, TensorFlow >= 2.0 ..." 的警告信息
- 增加了--version参数查看版本号

## V0.0.0.7

- 增加config选项，可通过config.json文件来启动模型
- 提升moe模型的速度

## V0.0.0.6

- 降低GLIBC版本，PIP安装包兼容更多系统
- PIP安装包支持更多架构（目前最低支持到SM_52）

## V0.0.0.5

- 修改文档，增加了一些pip安装后无法使用的情况说明
- 聊天模式下自动读取模型的生成配置文件
- 修复一些情况下kv_cache_limit计算错误的问题

## V0.0.0.4

- 增加ftllm run, chat, webui, server接口