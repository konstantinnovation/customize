# SSH KEY FIRST (ed25519)

`ssh-keygen -t ed25519 -C "unique name to identify this key."`


# General updates and coding font:
```
sudo apt update -y && sudo apt upgrade -y
sudo apt install curl fontconfig git zsh keychain gcc make open-jdk-21-jdk gnome-terminal
mkdir -p ~/.fonts && cd ~/.fonts || return
curl -LO https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Regular.ttf
curl -LO https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold.ttf
curl -LO https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Italic.ttf
curl -LO https://github.com/romkatv/powerlevel10k-media/raw/master/MesloLGS%20NF%20Bold%20Italic.ttf
fc-cache -f -v
sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)" -y
```

Restart your terminal emulator then change the font in your terminal to Meslo LGS NF

# add ~/bin to your path

In your bashrc, you can edit your PATH, or run this command:

`export PATH=$HOME/bin:$PATH`

If you installed oh-my-zsh, you can do the following instead:

```
sed -zi 's|# If you come from bash you might have to change your $PATH.|# If you come from bash you might have to change your $PATH.\nexport PATH=$HOME/bin:$PATH|g' ~/.zshrc
```

# oh-my-zsh plugins
```
git clone --depth=1 https://github.com/romkatv/powerlevel10k.git "${ZSH_CUSTOM:-${HOME}/.oh-my-zsh/custom}/themes/powerlevel10k"
sed -zi 's|ZSH_THEME="robbyrussell"|ZSH_THEME="powerlevel10k/powerlevel10k"|g' ~/.zshrc
sed -zi 's|plugins=(git)|plugins=(git zsh-autosuggestions zsh-syntax-highlighting keychain)\nzstyle :omz:plugins:keychain agents ssh\nzstyle :omz:plugins:keychain identities id_ed25519\nzstyle :omz:plugins:keychain options --quiet|g' ~/.zshrc
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
## NOTE: To selectively use keychain:

(for networks with a mounted home directory that would cause an immediate ssh key password prompt)
Disable the keychain plugin in .zshrc. Use an if statement and manually run it with a script like this:
```
# Allows for re-use of ssh-agent and/or gpg-agent between logins
/usr/bin/keychain --quiet $HOME/.ssh/id_ed25519
source $HOME/.keychain/$HOST-sh
```

# Kali full with desktop (for wsl):

```
sudo apt-get install kali-linux-full
sudo apt install -y kali-win-kex
```
### To start Win-KeX in Window mode with sound support, run either:

Inside of Kali WSL: `kex --win -s`

On Window’s command prompt: `wsl -d kali-linux kex --win -s`



