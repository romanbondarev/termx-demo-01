TermX use Github App for synchronization of the content with Github repositories.
Use separate Github App for every installation.


## Creating GitHub App
Follow the official Github documentation for [registering Github app](https://docs.github.com/en/apps/creating-github-apps/registering-a-github-app).

### termx-local-publisher
The example of configuration of local Github App publisher.
- GitHub App name: termx-local-publisher
- Homepage URL: https://github.com/apps/termx-local-publisher
- Callback URL: http://localhost:8200/github/cb
- Webhook -> active: false
- Repository permission
  - Contents: Read and write
  - Metadata: Read only

### Configuration of TermX-server application
Specify parameters bellow for termx-server docker
- GITHUB_APP_NAME=termx-local-publisher
- GITHUB_CLIENT_ID=$GeneratedClientId
- GITHUB_CLIENT_SECRET=$GeneratedSecret


### Install or reconfigure your GitHub App
If you need to install Github App to Github repositories or change permission then follow instructions below.
Follow the official Github documentation for [installing Github app](https://docs.github.com/en/apps/using-github-apps/installing-your-own-github-app).

Step-by-step guide
- In the upper-right corner of any page on GitHub, click your profile photo.
- Navigate to your account settings. ...
- In the left sidebar, click Developer settings.
- In the left sidebar, click GitHub Apps.
- Next to the GitHub App that you want to install, click Edit.
- Click Install App.
- Specify repositories to install.

