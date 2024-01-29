# Helm Push Action (OCI-based)
## 概述
&emsp;&emsp;用于在 GitHub Action 运行环境中将指定 Chart 推送到基于 OCI 的注册中心。使用此 Action 时，一般需要配合 Helm Login Action[[链接](https://github.com/marketplace/actions/helm-login-action-oci-based)]使用。

## 使用方法

```yaml
name: ci

on:
  push:

jobs:
  release:
    runs-on: ubuntu-latest
    steps:
      - name: Helm Setup
        uses: azure/setup-helm@v3
        with:
          version: 3.14.0
      - name: Login to DockerHub
        uses: central-x/helm-login-action@v1
        with:
          registry: registry-1.docker.io
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}
      - name: Push Helm Chart
        uses: central-x/helm-push-action@v1
        with:
          repository: oci://registry-1.docker.io/<username>
          chart: ./<path-to-chart>
```

## 自定义
### 输入参数（inputs）
&emsp;&emsp;以下输入参数可以用于 `steps.with`:

| 参数名称         | 类型     | 默认值 | 必选 | 描述                  |
|:-------------|--------|:----|:---|:--------------------|
| `repository` | String | 无   | 是  | 仓库地址                |
| `chart`      | String | 无   | 是  | 待推送的 Helm Chart 文件夹 |

