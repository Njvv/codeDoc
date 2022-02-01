# Mac

## 包管理：homebrew

### 一键下载

```bash
/bin/zsh -c "$(curl -fsSL https://gitee.com/cunkai/HomebrewCN/raw/master/Homebrew.sh)"
```

完成后可以跳过以下步骤，推荐选择清华镜像；

### 下载homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 设置brew/brew-core/brew-cask

```bash
git -C "$(brew --repo)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/brew.git

git -C "$(brew --repo homebrew/core)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-core.git

git -C "$(brew --repo homebrew/cask)" remote set-url origin https://mirrors.tuna.tsinghua.edu.cn/git/homebrew/homebrew-cask.git
```

### 设置homebrew-bottles

```bash
echo 'export HOMEBREW_BOTTLE_DOMAIN=https://mirrors.tuna.tsinghua.edu.cn/homebrew-bottles/bottles' >> ~/.zprofile
```

### 更新配置

```bash
source ~/.zprofile
```



## 终端：powerlevel10k

### 下载字体

推荐下载[`MesloLGS`](https://github.com/romkatv/powerlevel10k#manual-font-installation)字体，进入链接后依次下载四个字体；

不推荐`powerline`字体，会有乱码；

### 配置字体

终端 > 偏好设置 > 描述文件 > Basic；

调整字体为：MesloLGS；

### 下载powerlevel10k

```bash
brew install romkatv/powerlevel10k/powerlevel10k
echo "source $(brew --prefix)/opt/powerlevel10k/powerlevel10k.zsh-theme" >>~/.zshrc
```

### 更新配置

```bash
source ~/.zshrc
```

按照提示进行配置主题即可

### 重新配置

```bash
p10k configure
```

