# CosyVoice2-Ex-UI

基于 [journey-ad/CosyVoice2-Ex](https://github.com/journey-ad/CosyVoice2-Ex) 的离线优化版本，专为内网/无网络环境部署设计。

## 主要改动

### 1. 禁用 Google 字体
- 移除 Gradio 默认加载的 `Source Sans Pro` 和 `IBM Plex Mono` Google 字体
- 使用 `gr.themes.Base` 主题，字体改为本地系统字体 `Arial, PingFang SC, Microsoft YaHei`
- 页面加载不再依赖 `fonts.googleapis.com`

### 2. 禁用 modelscope 网络请求
- 注释 `cosyvoice/cli/cosyvoice.py` 中的 `from modelscope import snapshot_download`
- 注释 `webui.py` 中的 `snapshot_download()` 调用
- ASR 模型路径改为本地绝对路径

### 3. 其他优化
- `demo.launch()` 添加 `show_api=False` 减少外部资源加载

## 修改的文件

| 文件 | 修改内容 |
|------|----------|
| `webui.py` | 禁用 Google 字体、注释 snapshot_download、ASR 模型改本地路径 |
| `cosyvoice/cli/cosyvoice.py` | 注释 `from modelscope import snapshot_download` |

## 部署说明

### 前置条件
确保以下模型已下载到本地：
- CosyVoice2-0.5B 模型
- SenseVoiceSmall ASR 模型（放在 modelscope cache 目录）

### Docker 部署
```yaml
volumes:
  # 模型目录
  - /path/to/pretrained_models:/workspace/CosyVoice2-Ex/pretrained_models
  # modelscope cache（包含 SenseVoiceSmall）
  - /path/to/cache/modelscope:/root/.cache/modelscope
```

### 本地路径配置
`webui.py` 中 ASR 模型路径需要根据实际情况修改：
```python
model_dir = "/root/.cache/modelscope/hub/iic/SenseVoiceSmall"
```

## 原项目

- 原项目地址：https://github.com/journey-ad/CosyVoice2-Ex
- 原项目功能：CosyVoice2 功能扩充（预训练音色/3s极速复刻/自然语言控制/自动识别/音色保存/API）

## License

Apache 2.0（继承自原项目）
