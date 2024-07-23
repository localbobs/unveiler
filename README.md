https://app.appletsec.xyz/#document

### 什么是unveiler?

> `unveiler` 是一款小程序安全评估工具，支持小程序的代码审计和发现敏感信息泄露等安全问题

### ✅安装和使用

+   [下载](https://app.appletsec.xyz/#downloadList)对应系统的版本
+   [电报群](https://t.me/jsdebug) [自动发卡](https://shop.appletsec.xyz/prepage)

### 📝参数详解

| 子命令 | 参数 | 解释 |
| --- | --- | --- |
|  | `-l, --log-level <level>` | 设置日志等级 `debug`，`info`，`warn`，`error` 默认 `info` |
|  | `-v, --version` | 打印版本号并退出 |
|  | `-P, --profile` | 显示当前设备信息并退出 |
|  | `-T, --use-token <token>` | 消耗token增加可用时长并退出 |
|  | `-U, --update` | 检查更新和升级 |
|  | `-C, --clean-cache` | 清除缓存并退出 |
|  | `-X, --set-proxy <proxy>` | 手动配置代理，默认取 env.HTTPS\_PROXY |
|  | `--unset-proxy` | 取消配置代理 |
| `wx-hook` |  | 自动开启`devtools`并且过掉`checksum` |
| `wx` | `<packages...>` | 包的路径，可以是多个，也可以是一个目录 |
| `wx` | `-s, --scan-sensitive` | 开启敏感信息扫描 |
| `wx` | `-i, --appid <appid>` | 手动提供`appid` (仅在评估`windows`上的包时有效) |
| `wx` | `-f, --format` | 格式化输出 |
| `wx` | `--no-clear-parsed` | 解析后的残留文件将不会被清除 |
| `wx` | `--no-clear-save` | 不清除已经存在的解析结果 |
| `wx` | `--no-parse` | 只提取文件，但不会解析 |
| `wx` | `--clear-output` | 当输出目录不为空时程序将终止，提供该参数表示强制清空输出目录 |
| `wx` | `-d, --depth <depth>` | 设置从目录中查找深度，默认: `1` 设置为`0`时不限制深度 |
| `wx` | `-o, --output <path>` | 设置输出目录 |
| `wx` | `-p, --pack` | 将目录打包 |
| `wx` | `-w, --watch` | 监听将要打包的文件夹，并自动打包 |
| `wx` | `-e, --encrypt` | 将目录打包并加密 |
| `wx` | `-h, --help` | 打印帮助信息 |

### 📝常用示例

> 以下命令的 `unveiler` 只是示例，实际使用时根据具体情况替换，`windows` 可能是 `unveiler@xxx.exe`等等

#### 1.全局参数示例

+   代理可以自己指定，也会自动读取环境变量 https\_proxy (不区分大小写)
+   配置代理 `unveiler -X http://127.0.0.1:8080`
+   取消代理 `unveiler --unset-proxy`
+   查看设备信息 `unveiler -P`
+   检查更新版本 `unveiler -U`
+   清除程序缓存 `unveiler -C` (一般出现异常后尝试使用此参数)
+   使用token `unveiler -T xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`

#### 2.代码审计

> 现在解包相关的都需要带上 `wx` 子命令

+   常规使用 `unveiler wx /path/to/pkg/dir`
    
+   指定输出路径 `unveiler wx /path/to/pkg/dir -o /path/to/output/dir`
    
+   格式化输出结果 `unveiler wx -f /path/to/pkg/dir`
    

#### 3.敏感信息扫描

+   开始敏感信息扫描 `unveiler wx -sf /path/to/pkg/dir`

#### 4.打包功能的使用

+   目前比较稳定的打包是打包未被解析的源文件
+   所以建议整两套代码，一套用于审计，一套用于打包
+   目前只能每次打包一个文件
+   假设现在的目录为 `/path/to/pkg/__APP__.wxapkg`

1.  只提取单个包而不做解析 `unveiler wx --no-parse -f /path/to/pkg/__APP__.wxapkg -o /dist/__APP__`
2.  改动了代码之后在 `/dist/__APP__` 同步修改（自行搜索找到对应位置）
3.  开始打包 `unveiler -p /dist/__APP__`
4.  若要频繁修改建议使用 `-w` 参数，

+   可以在 `/dist/__APP__` 文件夹下有文件改动时将会自动打包
+   例如：`unveiler -wp /dist/__APP__`
+   打包后重新替换需要开启 `wx-hook`

#### 5\. 其他参数看[参数详解](https://app.appletsec.xyz/#%F0%9F%93%9D%E5%8F%82%E6%95%B0%E8%AF%A6%E8%A7%A3)