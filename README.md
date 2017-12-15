# kakaotalk-wine
카카오톡을 PlayOnLinux 없이 자동으로 설치하는 GUI installer이자 실행 스크립트입니다.

## Requirements
* `wine`
* `winetrick` (Optional)
* `gnutls` for i386
* `util-linux` (이미 대부분 설치되어 있음)
* `p7zip`
* `curl`
* `zenity`

### Arch Linux
```
$ sudo pacman -S lib32-gnutls wine-staging util-linux p7zip curl zenity
```
### Ubuntu
```
$ sudo dpkg --add-architecture i386
$ wget -nc https://dl.winehq.org/wine-builds/Release.key
$ sudo apt-key add Release.key
$ sudo apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
$ sudo apt update
$ sudo apt install --install-recommends winehq-staging
$ sudo apt install gnutls:i386 util-linux p7zip curl zenity
```

## How to install and run
```
$ ./kakaotalk
```

기타 기능이 궁금하면,
```
$ ./kakaotalk -h
```

## Winetricks
`winetrick`을 이용하여 오픈소스가 아닌 마이크로소프트의 라이브러리를 설치할 수 있습니다.

간혹 발생하는 오동작이나 동영상 / 그림 문제를 해결할 수 있습니다.
```
$ ./kakaotalk --install-trick
```

## 로그인이 안돼요 (너무 오래 걸려요, 오류가 나요)
```
$ ./kakaotalk -c
```
위 명령어로 Wine 설정을 실행한 뒤 `KakaoTalk.exe`에 대한 윈도우 버전이 XP인지 확인해 주세요.

`shell:InitNetworkAddressControl`이 Wine에서 구현되지 않아, Vista 이상의 윈도우 버전에서는 작동하지 않는 것으로 보입니다.

XP로 설정되어 있다면 될 때까지 로그인을 해주세요(..). 한 번 로그인이 되면 계속 잘 됩니다. 아마 네트워크 문제인 걸로 생각됩니다.

## Tested Environment
* Arch Linux x86-64 2017-12-15
* Wine 3.0rc1

## Known issues
* XP보다 높은 윈도우 버전에서 로그인 불가능
* 한 번에 로그인이 안되는 경우가 많음
* Wine 구버전에서 알림을 받을 때 Segmentation Fault
* Wine staging 2.21에서 실행 불가
* 사진을 전송하면 Segmentation Fault
* 간혹 아무것도 안했는데 갑자기 Segmentation Fault
* 그림자 기능이 활성화된 X Compositor(`compton` 등)에서 이상하게 보일 수 있음. Compositor 예외에 추가할 수 있음.
