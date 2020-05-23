# Essential Softwares


This features a non-exhaustive list of my Essential Softwares for PC.

## Common

### Coding

[**Visual Studio Code**](https://code.visualstudio.com/): general-purpose IDE for [Linux](https://code.visualstudio.com/docs/setup/linux) or Windows:

```shell
choco install -y vscode
```

## Windows 10

### General tools

[**Chocolatey**](https://chocolatey.org/install): command-line-based package manager

```powershell
# Open cmd or powershell in Administrative mode
Get-ExecutionPolicy
# If it returns Restricted, then run
Set-ExecutionPolicy AllSigned
# or
Set-ExecutionPolicy Bypass -Scope Process
# Install choco
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
# check
choco
```

[**7zip**](https://www.7-zip.org/download.html): compression and decompression tool

```shell
choco install -y 7zip
```

[**LockHunter**](https://lockhunter.com/startdownload.htm): find and kill processes occupying certain files. Unlocker is not longer supported.

```shell
choco install -y lockhunter
```

### Dictionaries

[**Lingoes**](http://www.lingoes.net/en/translator/download.htm): a dictionary reader

[**GoldenDict**](https://github.com/goldendict/goldendict/wiki/Early-Access-Builds-for-Windows): another dictionary reader

### Remote working

[**TeamViewer**](https://www.teamviewer.com/fr/telecharger/): connect to remote computers

```shell
choco install -y teamviewer
```

### Browsers

[**Google Chrome**](https://www.google.com/intl/fr/chrome/)

```shell
choco install -y googlechrome
```

### Security

[**Brave**](https://brave.com/fr/download/): Chromium-based browser with novel mechanism for ad filtering and tracker blocking

```shell
choco install -y brave
```

[**Tor**](https://www.torproject.org/download/): Firefox-based browser with emphasis on privacy

```shell
choco install -y tor-browser
```

[**Windscribe VPN**](https://windscribe.com/download): Canadian-based VPN service with 10GB/month for free users

```shell
choco install -y windscribe
```

[**Seed4me VPN**](https://seed4.me/pages/download): lightweight VPN but not free

## Linux

### Terminals

[**terminator**](https://terminator-gtk3.readthedocs.io/en/latest/) + [**oh-my-zsh**](https://ohmyz.sh/) or [**all-in-one instruction**](https://gist.github.com/renshuki/3cf3de6e7f00fa7e744a): enhanced terminal and z shell

[**vimrc**](https://github.com/amix/vimrc): ultimate vim configuration

### Shell tools

[**fasd**](https://www.tecmint.com/fasd-quick-access-to-linux-files-and-directories/)

[**silversearcher-ag**](https://github.com/ggreer/the_silver_searcher)

[**jq**](https://github.com/stedolan/jq): C-based JSON parser in shell. [An example](https://www.lewuathe.com/coloring-jq-with-less-command.html):

```bash
cat package.json | jq . -C | less -R
```

[**fx**](https://github.com/antonmedv/fx): JS-based JSON parser in shell

[**tldr**](https://github.com/tldr-pages/tldr): JS-based simplified and community-driven man pages

## iOS

### Languages

[**BBC Learning English**](https://www.bbc.co.uk/learningenglish/): beautiful English tutorials at beginner and intermediate level
