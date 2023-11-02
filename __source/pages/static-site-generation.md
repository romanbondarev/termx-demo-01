https://gitlab.com/kodality/terminology/termx-ssg

> **Docs in progress** 
> Will finish when is clear what I have done
{.is-warning}

## Github Actions
*.github/workflows/jekyll-docker.yml*
```yaml
name: Static Site Generation

on:
  push:
    branches: [ "main" ]

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Build the Jekyll site
        run: |
          docker run \
          -v ${{ github.workspace }}/__source:/__source -v ${{ github.workspace }}/_site:/template/_site  \
          docker.kodality.com/termx-jekyll-builder /bin/bash -c "chmod -R 777 ./_generate.sh && ./_generate.sh"

      - name: Upload _site
        uses: actions/upload-artifact@v3
        with:
          name: _site
          path: _site/**
```


### Steps
![](files/166/2023-11-02_13-52.png){width=800 .m-raised}

![](files/166/2023-11-02_13-53.png){width=800 .m-raised}

![](files/166/2023-11-02_13-54.png){width=800 .m-raised}