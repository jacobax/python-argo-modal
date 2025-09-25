# Modal 部署指南,会封号，勿用

1. 注册网站：[https://modal.com](https://modal.com)

2. 在个人资料页获取 API Token，例如：modal token set –token-id ak-XVbmGM9PF3TLwiu52 –token-secret as-Wo9a4CUsfGHkFu8q

3. 在 GitHub 仓库的 Settings → Secrets and variables → Actions 中，设置以下两个变量：

- `MODAL_TOKEN_ID`  
  这是你的 Modal Token ID，通常是以 `ak-` 开头的一串字符，比如 `ak-XVbmGM9PF3TLwiu52`。

- `MODAL_TOKEN_SECRET`  
  这是你的 Modal Token Secret，通常是以 `as-` 开头的一串字符，比如 `as-Wo9a4CUsfGHkFu8q7`。

4. 修改app.py里面的变量参数，deploy.py里面的app名字最好还是修改一下，最好让AI再修改一下。启动github action即可。
5.  节点获取说明：  
根据 UUID 和固定隧道域名手动配置，支持 vmess、vless、trojan 三种协议。

---

## 🌍 运行地域（Region）配置说明

在 `deploy.py` 文件中的第十八行：

```python
sandbox = modal.Sandbox.create(app=app, image=image, timeout=86400, region="us-west")
```
你可以根据实际需求修改 region="..." 来选择部署任务运行的地理位置。该参数影响执行延迟、合规性和数据传输速度等

### 🌐 Modal 支持的 Region 列表（含中英文说明）

| Broad 区域名     | Specific 具体区域 ID | 英文描述 / English Description | 中文说明 |
|------------------|----------------------|-------------------------------|----------|
| `us-east`        | `us-east-1`          | AWS Virginia                  | 亚马逊美国弗吉尼亚州（东部）|
|                  | `us-east-2`          | AWS Ohio                      | 亚马逊美国俄亥俄州           |
|                  | `us-east1`           | GCP South Carolina            | 谷歌云美国南卡罗来纳州       |
|                  | `us-east4`           | GCP Virginia                  | 谷歌云美国弗吉尼亚州         |
|                  | `us-east5`           | GCP Ohio                      | 谷歌云美国俄亥俄州           |
|                  | `us-ashburn-1`       | OCI Virginia                  | 甲骨文云美国弗吉尼亚州       |
| `us-central`     | `us-central1`        | GCP Iowa                      | 谷歌云美国艾奥瓦州           |
|                  | `us-chicago-1`       | OCI Chicago                   | 甲骨文云美国芝加哥           |
|                  | `us-phoenix-1`       | OCI Phoenix                   | 甲骨文云美国凤凰城           |
| `us-west`        | `us-west-1`          | AWS California                | 亚马逊美国加州（西部）       |
|                  | `us-west-2`          | AWS Oregon                    | 亚马逊美国俄勒冈州           |
|                  | `us-west1`           | GCP Oregon                    | 谷歌云美国俄勒冈州           |
|                  | `us-west3`           | GCP Utah                      | 谷歌云美国犹他州             |
|                  | `us-west4`           | GCP Nevada                    | 谷歌云美国内华达州           |
|                  | `us-sanjose-1`       | OCI San Jose                  | 甲骨文云美国圣何塞           |
| `eu-west`        | `eu-central-1`       | AWS Frankfurt                 | 亚马逊德国法兰克福           |
|                  | `eu-west-1`          | AWS Ireland                   | 亚马逊爱尔兰                 |
|                  | `eu-west-3`          | AWS Paris                     | 亚马逊法国巴黎               |
|                  | `europe-west1`       | GCP Belgium                   | 谷歌云比利时                 |
|                  | `europe-west3`       | GCP Frankfurt                 | 谷歌云德国法兰克福           |
|                  | `europe-west4`       | GCP Netherlands               | 谷歌云荷兰                   |
|                  | `eu-frankfurt-1`     | OCI Frankfurt                 | 甲骨文云德国法兰克福         |
|                  | `eu-paris-1`         | OCI Paris                     | 甲骨文云法国巴黎             |
| `eu-north`       | `eu-north-1`         | AWS Stockholm                 | 亚马逊瑞典斯德哥尔摩         |
| `ap-northeast`   | `asia-northeast3`    | GCP Seoul                     | 谷歌云韩国首尔               |
|                  | `asia-northeast1`    | GCP Tokyo                     | 谷歌云日本东京               |
|                  | `ap-northeast-1`     | AWS Tokyo                     | 亚马逊日本东京               |
|                  | `ap-northeast-3`     | AWS Osaka                     | 亚马逊日本大阪               |
| `ap-southeast`   | `asia-southeast1`    | GCP Singapore                 | 谷歌云新加坡                 |
|                  | `ap-southeast-3`     | AWS Jakarta                   | 亚马逊印度尼西亚雅加达       |
| `ap-south`       | `ap-south-1`         | AWS Mumbai                    | 亚马逊印度孟买               |
| `ca`             | `ca-central-1`       | AWS Montreal                  | 亚马逊加拿大蒙特利尔         |
|                  | `ca-toronto-1`       | OCI Toronto                   | 甲骨文云加拿大多伦多         |
| `uk`             | `uk-london-1`        | OCI London                    | 甲骨文云英国伦敦             |
|                  | `europe-west2`       | GCP London                    | 谷歌云英国伦敦               |
|                  | `eu-west-2`          | AWS London                    | 亚马逊英国伦敦               |
| `jp`             | `ap-northeast-1`     | AWS Tokyo                     | 亚马逊日本东京               |
|                  | `ap-northeast-3`     | AWS Osaka                     | 亚马逊日本大阪               |
|                  | `asia-northeast1`    | GCP Tokyo                     | 谷歌云日本东京               |
| `me`             | `me-west1`           | GCP Tel Aviv                  | 谷歌云以色列特拉维夫         |
| `sa`             | `sa-east-1`          | AWS São Paulo                 | 亚马逊巴西圣保罗             |

️ 示例：
将 region="us-west" 替换为 region="ap-southeast" 可将任务运行在新加坡或雅加达的数据中心。

更多详细地区，可以官网查看:https://modal.com/docs/guide/region-selection
## 感谢


特别感谢上游项目作者 eooce 的 py-argo 项目。
