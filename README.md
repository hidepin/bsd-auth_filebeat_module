bsd-auth_filebeat_module
============================================================

# 初期設定

1. filebeatをダウンロードし展開する

2. moduleディレクトリに移動する

    ```
    cd filebeat-x.x.x-linux-x86_64/module
    ```

3. cloneでbsd-auth moduleを追加する

    ```
    git clone https://github.com/hidepin/bsd-auth_filebeat_module.git bsd-auth
    cd ..
    ```

4. bsd-auth.ymlを作成する

    ```
    vi bsd-auth.yml
    ```

    ```
    filebeat.modules:

    - module: bsd-auth
      auth:
        enabled: true
        var.paths:
          - "/home/hidepin/auth-all.log*"

    output.elasticsearch:
      hosts: ["localhost:9200"]
      index: "bsd-auth-%{+yyyy.MM.dd}"
      template.name: "bsd-auth"
      template.path: "${path.config}/module/bsd-auth/config/bsd-auth.template.json"
    ```

## 実行

```
./filbeat -c bsd-auth.yml
```
