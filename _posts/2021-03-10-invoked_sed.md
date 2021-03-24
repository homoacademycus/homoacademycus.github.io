---
{"layout": "post", "categories": "TroubleShooting", "title": "invoked sed", "feature-img": "assets/img/feature_img.png"}
---
## Symtoms
tried to permit sed command only with root permission
```
chmod 750 /usr/bin/sed
```
then when use commands ls, mv ... related with file operation
```
$ ls .

bash: /usr/bin/sed: Permission denied
```
sed command is invoked everytime.

## Cause
The VTE uses this script to override the PROMPT_COMMAND in order to feed itself additional information via terminal control codes. 
In particular, this script is used to tell the VTE the current directory of the shell.
Previously the VTE component used to read this from /proc/<pid>/cwd however according to VTE upstream there were a number of issues with this approach and hence the change to /etc/profile.d/vte.sh.

- /etc/profile.d/vte.sh
```
case "$TERM" in
  xterm*|vte*)
    [ -n "$BASH_VERSION" ] && PROMPT_COMMAND="__vte_prompt_command"
    [ -n "$ZSH_VERSION"  ] && precmd_functions+=(__vte_osc7)
    ;;
esac
vte_prompt_command() {
  ######### HERE : bash tries to look up comletions with sed ########
  local command=$(HISTTIMEFORMAT= history 1 | sed 's/^ *[0-9]\+ *//')
  ###################################################################
  command="${command//;/ }"
  local pwd='~'
  [ "$PWD" != "$HOME" ] && pwd=${PWD/#$HOME\//\~\/}
  printf "\033]777;notify;Command completed;%s\007\033]0;%s@%s:%s\007%s" "${command}" "${USER}" "${HOSTNAME%%.*}" "${pwd}" "$(__vte_osc7)"
}
```

## Solution
1. in vte.sh delete this(then you must use correct filename)
```
sed 's/^ *[0-9]\+ *//'
```
fixed!

2. use command to ignore aliases and functions to explicitly run the builtin or executable directly
```
ls() {
    command ls --color=auto
}
```

