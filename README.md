qiniu-autosync
==============

Sync files to Qiniu Cloud Storage automaticly with inotify-tools

此脚本可监控 Linux/Unix 上指定的文件夹，并将此文件夹内的新增或改动文件自动同步到七牛云存储，可设定同步删除。

安装
====

1. 需先安装 inotify-tools - <https://github.com/rvoicilas/inotify-tools/wiki>
2. 然后下载 qboxrsctl - <http://docs.qiniutek.com/v3/tools/qboxrsctl/>
3. 下载脚本 qiniu-autosync.sh

```
curl -fsSkL https://raw.github.com/why404/qiniu-autosync/master/qiniu-autosync.sh -o qiniu-autosync.sh
chmod +x ./qiniu-autosync.sh
```

使用
====

获取七牛云存储 ACCESS_KEY 和 SECRET_KEY 以及 BUCKET_NAME (空间名称) 请登录：<https://dev.qiniutek.com>

用法（反斜杠用于排版换行需要，实际情况下可忽略）:

```
./qiniu-autosync.sh -a /PATH/TO/appkey.json \     # appkey.json 写明 {"access_key":"YOUR_ACCESS_KEY", "secret_key": "YOUR_SECRET_KEY"}
                    -b BUCKET_NAME \              # 用于存储文件的七牛空间名称
                    -c /PATH/TO/qboxrsctl \       # qboxrsctl 可执行命令所在路径
                    -d /PATH/TO/WATCH_DIR \       # 要监控的目录，绝对路径
                    -e ALLOW_DELETE_TrueOrFalse \ # 是否允许自动删除，缺省为 false
                    -f FILE_BLOCK_SIZE \          # 文件切片分块大小，超过这个大小启用并行断点续上传，缺省为 4194304 (4MB)
                    -g INOTIFY_IGNORE_PATTERN     # 忽略列表(正则)，缺省为 "^(.+(\~|\.sw.?)|4913)$" (即 vim 临时文件)
```
