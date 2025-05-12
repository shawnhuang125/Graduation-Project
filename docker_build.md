# flask應用docker打包指南
- 建構`docker image`
```
docker build -t [專案名稱] [目錄位置]
```
- 建構名為`mapapiapplication`的`docker image`,在專案根目錄
```
docker build -t mapapiapplication .
```
- `docker image`儲存`.tar`檔案
```
docker save -o [輸出檔案名稱.tar] [docker image name]
```
- 將名為`mapapiapplication`的`docker image`儲存為`mapapiapplication.tar`
```
docker save -o mapapiapplication.tar mapapiapplication                                                                                                                                                                                                                                              
```
- 使用windows內建的壓縮工具壓縮`docker image`
```
Compress-Archive -Path mapapiapplication.tar -DestinationPath mapapiapplication.zip 
```
- 使用windows內建的壓縮工具壓縮`mapapiapplication.tar`輸出檔案為`mapapiapplication.zip`
```
Compress-Archive -Path mapapiapplication.tar -DestinationPath mapapiapplication.zip 
```
