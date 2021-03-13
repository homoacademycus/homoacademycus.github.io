---
{"layout": "post", "categories": "TroubleShooting", "title": "vscode IBUS", "feature-img": "assets/img/feature_img.png"}
---
# symtoms
```
한영 전환키가 vscode 에서만 동작 안함
```

# cause
```
iBus는 vscode와 Atom에서 작동 안함. snap 데몬 접근을 막는다는 이슈도 보임.
```

# solution
1. ctrl+space를 ibus의 한영키에 등록해서 사용
2. 다른 편집기인 UIM을 시스템에 설치해서 사용
```
sudo apt install uim

// 오른쪽 Alt 키의 기본 키 맵핑을 제거하고 'Hangul'키로 맵핑
$ xmodmap -e 'remove mod1 = Alt_R'
$ xmodmap -e 'keycode 108 = Hangul'
// 키 맵핑 저장
$ xmodmap -pke > ~/.Xmodmap
$ xmodmap -e 'keycode 108 = Hangul'
$ xmodmap -pke > ~/.Xmodmap
```

3. vscode 설정에서 키 (R-alt)를 누를때 포커스 설정 해제
```
Custom Menu Bar Alt Focus
Enable Menu Bar Mnemonics
```
All keyboard shortcuts in VS Code can be customized via the keybindings. json file. To configure keyboard shortcuts through the JSON file, open Keyboard Shortcuts editor and select the Open Keyboard Shortcuts (JSON) button on the right of the editor title bar. This will open your keybindings.

# related
1. UI에서 보이는 locale 설정(한글팩 설치)
```
Configure Display Language
```

# English
It is known that IBUS's custom keymap doesn't work on vscode. There is issue that vscode's access to snap daemon is prohibited. In my case, I just use default(well-known) IBUS key map to change my input source (ctrl+space). 

Let me introduce what you can try.
1. install another text editor not IBUS
```
sudo apt install uim
$ xmodmap -e 'remove mod1 = Alt_R'
$ xmodmap -e 'keycode 108 = Hangul'
$ xmodmap -pke > ~/.Xmodmap
$ xmodmap -e 'keycode 108 = Hangul'
$ xmodmap -pke > ~/.Xmodmap
```

2. you can set custom key mapping on vscode
```
find these in vscode's settings menu
keyboard
keybinding
```
All keyboard shortcuts in VS Code can be customized via the keybindings. json file. To configure keyboard shortcuts through the JSON file, open Keyboard Shortcuts editor and select the Open Keyboard Shortcuts (JSON) button on the right of the editor title bar. This will open your keybindings.
```

