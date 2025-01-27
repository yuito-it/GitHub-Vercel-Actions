# GitHub-Vercel-Actions

GitHub OrganizationなどでVercelが使えないときに使って下さい。

## 使い方

変数にこれらの値をいれてください。
withで構いません。

- `vercel-token` - Vercel API token
- `vercel-project` - Vercel Project Name

また、これを用いて、DeploymentURLを設定することもできます。

### Exsample

```yaml
name: Vercel Production Deployment
on:
  push:
    branches:
      - main
jobs:
  deployment:
    runs-on: ubuntu-latest
    concurrency: Production
    environment:
        name: Production
        url: ${{ steps.get_release_url.outputs.release_url }}
    steps:
    - uses: yuito-it/GitHub-Vercel-Actions@v1.0.0
      with:
        vercel-token: ${{ secrets.VERCEL_TOKEN }}
        vercel-project: ${{ vars.VERCEL_PROJECT }}
    - name: Set release url
      shell: bash
      id: get_release_url
      run: echo release_url=$(cat deployment-url.txt) >> $GITHUB_OUTPUT
```
