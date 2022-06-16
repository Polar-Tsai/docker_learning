# docker_learning
[教學簡報](https://www.canva.com/design/DAFDEWeuvlg/omFE2zdIRsJC5Oq8keFXVw/view?utm_content=DAFDEWeuvlg&utm_campaign=designshare&utm_medium=link&utm_source=publishsharelink)

# My Docker Hub

https://hub.docker.com/repository/registry-1.docker.io/polar1244/chinatimes_webcrawler/general

# 線上的測試環境 
謝謝Jason大大找到的資源

https://labs.play-with-docker.com/


# 技術分享的 docker 指令
1. 從雲端下載 docker image

`docker image pull polar1244/chinatimes_webcrawler:v4`

2. 運行剛剛下載的 image

`docker run polar1244/chinatimes_webcrawler:v4`

3. 利用volume與OS串接資料

`docker run -name c012 -v ~/docker_volume:/docker_test/data polar1244/chinatimes_webcrawler:v4`

4. 在cmd查看文件

`cat 2022-06-16.csv`

5. 查看 image 清單

`docker image ls`
`docker images`

6. 刪除image

`docker rmi <IMAGE ID>` 


# 常見的 docker 指令
### image上的建立、上傳與刪除

在地端建立與使用docker image
```
docker build -t(給予file名稱) 帳號名/image名稱 .(查看本地當下的目錄)
docker images #查看是否成功建立image
docker container run 完整image名稱 #檢查是否真的從dockerfile安裝好image
```
上傳image至雲端
```
docker images #查看目前的image目錄
docker login/logout #登出/登入
docker push account/imagename #上傳指定image
```
清理本地檔案
```
docker rmi -f(強制執行，不管是不是正在container使用) <IMAGE ID>
```


### Container上的建立、執行與清除

使用與建立container
```
docker container ls #查看所有container資料
docker pull alpine #下載alpine image
docker images #查閱目前的images目錄
docker (container) run --name c001(將這個container命名) alpine(使用哪個image執行) ls /(列出所有的檔案與目錄)
```
在虛有程序中執行container
```
docker run -it --name c003(container's name) alpine /bin/sh(虛有程序) #出現"/ # "就代表執行成功
/ # ls #在"/ #"虛有程序中執行查看檔案位置
/ # exit #離開虛有程序
```
永久執行container
```
docker run -d(讓他像daemon一樣永遠執行) --name c004 alpine tail -f(追蹤指定file的log，並將其印到console上) /dev/null
docker exec(在指定container ID執行一個"/bin/sh"的新程序) -it (container ID) /bin/sh #出現"/ # "就代表執行成功
/ # ls
/ # exit
docker container ls #container依然在背景執行
```
想利用VM Linux主機IP 開啟nginx
```
docker pull nginx:latest(選擇最新版本)
docker run -d(於背景執行) -p 8081:80(Linux版才做。此指port mapping) --name c006 nginx
```
關於port(連接埠)
- 8081: vm Linux port
- 80:  nginx web server所使用的port
- echo $(docker-machine ip) #取得VM Linux主機IP
- 將VM Linux主機IP輸入在網頁再加上.8081，就能進入nginx頁面

清除Container
```
docker container ls #查看container
docker container stop (container ID) #停止container執行
docker container rm (container id) #刪除container
docker container ls -a #檢查所有container 
```

### Dockerfile建立

`docker image build --tag <docker image name> .`

更改image名稱

`docker tag <IMAGE ID> <USER ID/DOCKER NAME>`

