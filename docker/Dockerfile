#FROM taylor_nvidia-cuda11.8.0-torch2.0.1-devel:latest
FROM taylor_cuda11.8.0_torch2.0.1_fastapi-devel:latest
# 镜像里面是Python 3.10.6  | torch==2.0.1

LABEL version="1.0" date="2024-01-31 10:11"
LABEL baseimages="taylor_cuda11.8.0_torch2.0.1_fastapi-devel:latest"
LABEL maintainer="taylor.he@ferban.com"


# ==================================================================
# starchat python env
# https://huggingface.co/HuggingFaceH4/starchat-beta
# ------------------------------------------------------------------
COPY requirements.txt /workspace/requirements.txt

RUN chmod +x /workspace/requirements.txt \
&& pip3 config set global.index-url  https://pypi.tuna.tsinghua.edu.cn/simple/ \
&& pip3 config set install.trusted-host pypi.tuna.tsinghua.edu.cn \
&& pip3 config --user set global.progress_bar off \
#&& pip3 config set global.index-url http://mirrors.aliyun.com/pypi/simple/ \
#&& pip3 config set install.trusted-host mirrors.aliyun.com \
&& python3 -m pip install --upgrade pip

RUN pip3 install --no-cache-dir -r /workspace/requirements.txt

# 解决加载文档时出错：libGL.so.1: cannot open shared object file
RUN apt update && apt install libgl1-mesa-glx -y
# ==================================================================

RUN echo "export TF_ENABLE_ONEDNN_OPTS=0" >> /etc/profile

COPY farai_knowledge_chat_server /workspace/farai_knowledge_chat_server

RUN chmod +x /workspace/farai_knowledge_chat_server

WORKDIR /workspace/farai_knowledge_chat_server/

ENTRYPOINT ["python3", "startup.py", "-a"]
# ==================================================================