# 项目说明  
本项目参考LangChain-Chatchat项目实现：  
1. 基于0.2.10版本更新。  
2. 删除了search和agent功能。  
3. 根据项目需求添加了一部分接口(保留了知识库相关原始接口)。
4. 服务打包镜像部署。  

原始项目说明参见：📃 [original.md](original.md)  
镜像打包部署命令参考：📃 [run.md](docker/run.md)  

项目代码参考地址：  
[LangChain-Chatchat](https://github.com/chatchat-space/Langchain-Chatchat)  
[QAnything](https://github.com/netease-youdao/QAnything)

部署说明：  
1. 与后端代码约定数据分部式存储地址为：/data/release/juicefs，因服务使用容器化部署所以需要挂载目录并映射到相同路径：  
   -v /data/release/juicefs:/data/release/juicefs   
2. 默认使用模型以及模型存储地址：  
   m3e-base: /data/release/juicefs/models/m3e-base  
   chatglm3-6b: /data/release/juicefs/models/chatglm3-6b  


TODO:
1. 更新接口解决上传同名文件覆盖问题；  
2. 上传文件路径做数据向量化
2. 上传的是文件夹路径，要做批量数据的向量化
2. ......  
