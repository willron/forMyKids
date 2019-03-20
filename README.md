# forMyKids

### 学习

#### yysz.html
配合妈妈做的汉字卡和小孩玩游戏：
把汉字卡字朝上散放在桌面，打开页面，在文本框输入汉字卡上面所有汉字。点开始跟停止，会随机出一个汉字，小孩大人看谁更快找到卡，找到后要念出是什么字。
当然，如果小孩完成了应该得到比大人更多的分数才公平。

有条件的话，请使用web服务器做部署并使用正确的配置，将获得拼音显示跟读音功能。Nginx为例：
```nginx
server {
    listen 80;
    server_name yysz.example.com;
    root /path/to/file;
    index yysz.html index.html;
    
    # 反向代理到海词
    location /dict/ {
        proxy_pass http://hanyu.dict.cn/;
        proxy_set_header  Host  hanyu.dict.cn;
        proxy_set_header  User-Agent  "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/71.0.3578.98 Safari/537.36";
        proxy_set_header  Referer  http://hanyu.dict.cn/;
    }
}
```
