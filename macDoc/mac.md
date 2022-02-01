# Mac

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

