<h1><b> Docker部署 </h1></b>

**卸载旧版本：**

```
#shell
sudo dnf remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
```

**更新dnf：**

```
#shell
sudo dnf upgrade -y
```

**安装dnf-olugins-core包并设置储存库：**

```
#shell
sudo dnf -y install dnf-plugins-core
sudo dnf config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

**配置DNS并重启：**
<br>手动配置：DNS：223.5.5.5,180.76.76.76

**安装docker：**
<br>
- **安装最新版本：**
- ```
  #shell
  sudo dnf install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin -y
  ```



- **安装指定版本：**
- ```
  #shell
  dnf list docker-ce --showduplicates | sort -r
			# 注：列出存储库中的可用版本
  sudo dnf install docker-ce-<VERSION_STRING> docker-ce-cli-<VERSION_STRING> containerd.io docker-buildx-plugin docker-compose-plugin
  ```

**启动docker：**

```
#shell
sudo systemctl start docker
sudo systemctl enable --now docker
```

**配置加速 ：**

```
#shell
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-"EOF"
{

"max-concurrent-downloads": 20,

"log-driver": "json-file",

"log-level": "warn",

"log-opts": {

"max-size": "10m",

"max-file": "3"

},

"exec-opts": [

"native.cgroupdriver=systemd"

],

"registry-mirrors": [
"https://docker.1panel.live/",
"https://docker.registry.cyou",
"https://docker-cf.registry.cyou",
"https://dockercf.jsdelivr.fyi",
"https://docker.jsdelivr.fyi",
"https://dockertest.jsdelivr.fyi",
"https://mirror.aliyuncs.com",
"https://dockerproxy.com",
"https://mirror.baidubce.com",
"https://docker.m.daocloud.io",
"https://docker.nju.edu.cn",
"https://docker.mirrors.sjtug.sjtu.edu.cn",
"https://docker.mirrors.sjtug.sjtu.edu.cn",
"https://docker.mirrors.ustc.edu.cn",
"https://mirror.iscas.ac.cn",
"https://docker.rainbond.cc",
"https://do.nark.eu.org",
"https://dc.j8.work",
"https://dockerproxy.com",
"https://gst6rzl9.mirror.aliyuncs.com",
"https://registry.docker-cn.com",
"http://hub-mirror.c.163.com",
"http://mirrors.ustc.edu.cn/",
"https://mirrors.tuna.tsinghua.edu.cn/",
"http://mirrors.sohu.com/",
"https://82m9ar63.mirror.aliyuncs.com/",
"https://mirror.example.com"
],

"insecure-registries": [

"sealos.hub:5000","192.168.142.10"

],

"data-root": "/var/lib/docker"
}
EOF
```

**重启该服务和配置文件 ：**

```
#shell
sudo systemctl daemon-reload
sudo systemctl restart docker
```

**测试是否成功安装docker：**

```
#shell
sudo docker run hello-world
```
