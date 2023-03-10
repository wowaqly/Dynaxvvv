# 腾讯云cos-backup
每12小时增量同步一次文件夹中的文件到cos,需要立即增量同步restart一次容器即可

⚠️注意，因为cos的特性，不会同步文件夹中的二级文件夹及其中的文件。

``` shell
docker run -d --restart=unless-stopped \
--name cosbak \
-e BUCKETNAME_APPID=123 \
-e SECRETID=123id \
-e SECRETKEY=123key \
-e REGION=ap-nanjing \
-e COS_PATH=/ \
-v /xxx/xxx:/root/data \
wowaqly/cos_backup
```
## 参数
|名称               |说明                                                   |
|:-                 |:-                                                     |
|BUCKETNAME_APPID |存储桶名称|
|SECRETID | 腾讯云账号密钥ID 建议使用子账号 最小权限|
|SECRETKEY | 腾讯云账号密钥KEY 建议使用子账号 最小权限|
|REGION |地域简称 默认ap-nanjing|
|COS_PATH|同步到cos储存桶中的路径 默认 /|

*参数设置，请参考：<https://cloud.tencent.com/document/product/436/10976>*

