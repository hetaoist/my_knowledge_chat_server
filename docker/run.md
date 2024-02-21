# root@10.18.50.89:
scp -r /data/user/taylor/Code/docker  root@10.18.61.35:/data/user/Taylor/Code/

# root@10.18.61.35:
cd /data/user/Taylor/Code/docker/farai_knowledge_chat_server_release  

sudo docker tag farai_knowledge_chat_server_release:latest farai_knowledge_chat_server_release:v20240219  
sudo docker build -f Dockerfile -t farai_knowledge_chat_server_release:latest .  

# 挂载代码方式的部署开发环境 10.18.61.35
docker run -itd \
--gpus '"device=5"' \
--runtime=nvidia \
--restart always \
--ipc=host \
-v /data/release:/data/release \
--name farai_knowledge_chat_server_release \
-p 40300:12345 \
-p 40322:22 \
-p 48501:8501 \
-p 47861:7861 \
-p 40000:20000 \
-p 40001:20001 \
-p 40002:20002 \
--ulimit memlock=-1 \
farai_knowledge_chat_server_release:latest  

# root@10.18.50.89
docker run -itd \
--runtime=nvidia \
--gpus all \
--restart always \
--ipc=host \
-v /data/release:/data/release \
--name farai_knowledge_chat_server_release \
-p 40300:12345 \
-p 40322:22 \
-p 8501:8501 \
-p 7861:7861 \
-p 20000:20000 \
-p 20001:20001 \
-p 20002:20002 \
--ulimit memlock=-1 \
--privileged=true \
farai_knowledge_chat_server_release:latest  


-e NVIDIA_VISIBLE_DEVICES=1,2 \
--gpus '"device=5"' \
--gpus all \
docker logs -f farai_knowledge_chat_server_release  

docker exec -it farai_knowledge_chat_server_release bash  
docker rm -f farai_knowledge_chat_server_release  

docker save -o farai_knowledge_chat_server_release.tar farai_knowledge_chat_server_release:latest
scp -r farai_knowledge_chat_server_release.tar  root@10.18.61.35:/data/release/
docker load -i farai_knowledge_chat_server_release.tar

scp -r /data/release/m3e-base  root@10.18.61.35:/data/release/
scp -r /data/release/chatglm3-6b  root@10.18.61.35:/data/release/








