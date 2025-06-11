sudo dnf install docker  
sudo yum install docker   
sudo service docker start  && sudo systemctl  enable docker  

sudo usermod -a -G docker user   
newgrp docker  

Currently the accepted answer does not work for me but the following does:  

sudo curl -SL https://github.com/docker/compose/releases/download/v2.32.4/docker-compose-linux-$(uname -m) -o /usr/local/bin/docker-compose \
&& sudo chmod +x /usr/local/bin/docker-compose  

##  
初始化 Swarm  
docker swarm init \ &&
docker stack deploy -c docker-compose.yml mystack  
# 更新
docker service update --force mystack_web  
docker ps -a --filter name=mystack_web  
docker stack rm mystack  
docker stack deploy -c docker-compose.yml mystack  
