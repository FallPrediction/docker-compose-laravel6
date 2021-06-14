# docker-compose-laravel6
## 使用臨時composer容器建立laravel6專案
docker composer官方[文檔](https://hub.docker.com/_/composer?tab=description)
```
docker run --rm -v $(pwd):/app composer  create-project --prefer-dist laravel/laravel 專案名稱 "6.*"
```

修改目錄及檔案權限
https://stackoverflow.com/questions/30639174/how-to-set-up-file-permissions-for-laravel
```
sudo chown -R www-data:www-data 專案路徑
```
把使用者加入www-data群組裡，僅需執行一次
```
sudo usermod -a -G www-data 使用者名稱
```
```
cd 專案路徑
sudo find . -type f -exec chmod 664 {} \;
sudo find . -type d -exec chmod 775 {} \;
```

## 建立docker-compose.yml
注意php及nginx的volume專案目錄，以及mysql的密碼


## laravel專案.env檔
1. DB_HOST改為mysql容器名稱
2. DB_PASSWORD改為在docker-compose.yml中設定的密碼

## vscode xdebug
.vscode/launch.json
```
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Listen for XDebug",
            "type": "php",
            "request": "launch",
            "port": 9003,
            "pathMappings": {
                "/var/www/html/": "${workspaceRoot}"
            },
            "hostname": "localhost"
        }
    ]
}
```
