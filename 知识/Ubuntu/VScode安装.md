## 使用 apt 安装 Visual Studio Code

Visual Studio Code 在官方的微软 Apt 源仓库中可用。想要安装它，按照下面的步骤来：

01.以 sudo 用户身份运行下面的命令，更新软件包索引，并且安装依赖软件：

```text
sudo apt update
sudo apt install software-properties-common apt-transport-https wget
```

02.使用 wget 命令插入 Microsoft GPG key ：

```text
wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | sudo apt-key add -
```

启用 Visual Studio Code 源仓库，输入：

```text
sudo add-apt-repository "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main"
```

03.一旦 apt 软件源被启用，安装 Visual Studio Code 软件包：

```text
sudo apt install code
```

当一个新版本被发布时，你可以通过你的桌面标准软件工具，或者在你的终端运行命令，来升级 Visual Studio Code 软件包：

```text
sudo apt update
sudo apt upgrade
```