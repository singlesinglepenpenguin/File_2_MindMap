# File_2_MindMap
Upload file to get markdown, get mindmap with Mermaid, post request and get LLM output from aliyun. 

## Config
Remember to input your own api key in the next.config.ts.

## Flow chat
```mermaid
flowchart TD
    A["开始"] --> B["用户选择文件"]
    B --> C["用户上传文件"]
    C --> D["用户前端输入分片token数"]
    D --> E["切分文档为分片列表"]
    E --> F{"分片列表是否为空?"}
    F -- 否:::no --> G["取出当前分片"]
    G --> H["组装请求LLM提示词"]
    H --> I["HTTP请求LLM生成/更新思维导图"]
    I --> J["标准化思维导图JSON"]
    J -- 上一轮输出:::feedback --> H
    J --> K["递归处理JSON生成Mermaid图像"] & M["通过LLM生成Markdown"]
    K --> L["显示/保存Mermaid图"]
    M --> N["生成Xmind可编辑文件"]
    N --> O["本轮循环结束"]
    L --> O
    O --> F
    F -- 是:::yes --> P["结束"]
```