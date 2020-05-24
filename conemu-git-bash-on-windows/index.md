# Multi-windows Linux-like terminal on Windows


The frustration of having a Linux-like terminal with bash environment for development purpose has been lingering for a while.
There are currently many terminal softwares such as HyperTerminal, ConEmu, Cmder, Cygwin and console application such as git
bash, WSL, msys, powershell.

As a fan of terminator, bash, and oh-my-zsh stack in Linux, I had problems switching to Windows. For Windows, WSL provide a real Linux bash
environment, however, its integration with oh-my-zsh library has some font and background problems.

For the moment, I prefer using git bash as my favorite console, which satisfies my need for git commands and some vim editing.
I particularly like the Ctrl+Insert keyboard shortcut for pasting texts. However, it lacks multi-windows functionality and
multi-tabs. This moment, ConEmu comes into play.

This guides provide an instruction on how to integrate git bash with ConEmu to have a multi-view window and a multi-tab environment.

## Procedure

### Install git bash

```bash
choco install git
```

Add configuration to `.bashrc`: TBD

### Add `z` for fast navigation
There are many directory navigation tools around, [`fasd`](https://github.com/clvv/fasd), [`z`](https://github.com/rupa/z), [`autojump`](https://github.com/wting/autojump), `wd` (oh-my-zsh plugin), [posz](https://github.com/manojlds/posz).
Many of them are optimized for Linux environment. In git bash, the appropriate tool for an easy integration is `z`.

```bash
cd ~
git clone https://github.com/rupa/z
echo '# jump around directories' > ~/.bashrc
echo '. /c/Users/$(whoami)/z.sh' > ~/.bashrc
echo 'set $_Z_MAX_SCORE 100 # default 9000' > ~/.bashrc
```

![General settings](/conemu-git-bash-on-windows/conemu-git-bashrc.png)

### Install ConEmu using [chocolatey](https://chocolatey.org/packages/ConEmu)

```bash
# Run the command in Windows command prompt
choco install conemu
```

ConEmu settings:

- TL-DR: import the [XML setting file](/conemu-git-bash-on-windows/conemu-settings.xml)
- General -> Font: choose `Consolas` size 12 if integrating git bash
  - If WSL bash environment is also integrated, install powerline font and choose `Droid Sans Mono Slashed for Pow`

![General settings](/conemu-git-bash-on-windows/conemu-general-font-setting.png)

- General -> Confirm: uncheck all checkboxes in `Close confirmations` section

![General settings](/conemu-git-bash-on-windows/conemu-general-confirm.png)

- Startup -> Tasks:
  - Add a new task `Git Bash`
  - Assign a hotkey `Ctrl+Shift+T`
  - Check `Default task for new console`, check `Default shell`
  - Add launch command: `"C:\Program Files\Git\bin\sh.exe" --login -i`

![General settings](/conemu-git-bash-on-windows/conemu-task-setting.png)

- Startup: ensure `Specified named task` to be `{Git Bash}`

![General settings](/conemu-git-bash-on-windows/conemu-startup-setting.png)

- Keys & Macro: keys are expected to comply with Linux's terminator
  - `Ctrl+Shift+W`: Close active console
  - `Ctrl+Shift+E`: *split* the view vertically (already default)
  - `Ctrl+Shift+O`: *split* the view horizontally (already default)

![General settings](/conemu-git-bash-on-windows/conemu-key-and-macro.png)

- General:
  - Choose `{Git Bash}` in `Choose the startup task or even a shell with arguments`
  - Choose `<Babun>` color scheme

![General settings](/conemu-git-bash-on-windows/conemu-general-setting.png)

