# kakaotalk-wine
카카오톡을 리눅스에서 사용할 수 있도록 합니다.

PlayOnLinux 없이 자동으로 설치하는 standalone GUI installer이자 실행 스크립트입니다.

## Requirements
* `wine` (최신 개발 버전 추천)
* `winetrick` (Optional)
* `gnutls` for i386
* `p7zip`
* `curl`
* `zenity`

### Arch Linux
```
(multilib repo가 활성화되어있어야 함)
$ sudo pacman -S lib32-gnutls wine p7zip curl zenity
```
### Ubuntu
```
(Wine 개발 버전 설치)
$ sudo dpkg --add-architecture i386
$ wget -nc https://dl.winehq.org/wine-builds/Release.key
$ sudo apt-key add Release.key
$ sudo apt-add-repository https://dl.winehq.org/wine-builds/ubuntu/
$ sudo apt update
$ sudo apt install --install-recommends winehq-devel
(Dependency 설치)
$ sudo apt install gnutls:i386 p7zip curl zenity
```

## How to install and run
따로 카카오톡 인스톨러를 다운받을 필요가 없습니다.
```
$ ./kakaotalk
```

## Winetricks
`winetrick`을 이용하여 오픈소스가 아닌 마이크로소프트의 라이브러리를 설치할 수 있습니다.

```
$ ./kakaotalk --install-trick
```

일반적으로 설치하지 않아도 잘 작동하지만, 간혹 오동작이 발생하거나 동영상 / 그림 문제가 있다면 설치해보세요.

## 로그인이 안돼요 (너무 오래 걸려요, 오류가 나요)

될 때까지 로그인을 해주세요(..) 한 번 로그인이 되면 계속 잘 됩니다.

처음 로그인 후 서버 오류가 발생하는 것을 본 뒤, 완전히 종료 후 다시 로그인하면 대부분 해결됩니다.

## 폰트 / 언어를 바꾸고 싶어요
설정에서 간혹 폰트 드랍다운이 열리지 않는 경우가 있습니다. 그리고 설정에서는 언어를 바꾸는 옵션이 없습니다. 다음 파일을 수정하여 수동으로 지정해줄 수 있습니다.

```
~/.kakaotalk/wine/drive_c/users/<User Name>/Local Settings/Application Data/Kakao/KakaoTalk/talk_pref.ini
```
```
[KAKAO_TALK]
LANG=en
set_auto_start=no
main_hwnd=4002a
CustomFontFaceName=Arial
set_auto_login=no
```
`LANG`을 `ko`로, `CustomFontFaceName`을 한글 폰트(예: `NanumGothic`)로 바꿔주세요.

## 업데이트 후 오류가 생겨요
다음 명령어로 재설치를 해보세요.
```
$ ./kakaotalk --reinstall
```

## Terminal 말고 메뉴나 바로가기로 바로 실행하고 싶어요
[Desktop Entry](https://wiki.archlinux.org/index.php/desktop_entries)를 추가해보세요.

## Tested Environment
* Arch Linux x86-64 2017-12-15
* Wine 3.0rc1
* Uim 입력기 (uim-byeoru)

## What's Working (Wine 3.0rc1)
* 채팅 보내기 / 받기
* 한글 입력
* 소리 재생
* 알림
* 시스템 트레이 아이콘
* 기타 등등..

## Known issues (Wine 3.0rc1)
* 그림자 기능이 활성화된 X Compositor(`compton` 등)에서 이상하게 보일 수 있음
* 몇몇 이모티콘이 보이지 않거나 로딩이 느림
* 로그인 에러가 잦음
* 몇몇 그림 파일을 볼 수 없음
* 그림 보내기 불가
* 특정 단톡방에 들어가면 Segmentation Fault
* 간혹 알림을 받으면 Segmentation Fault
* 간혹 아무것도 안했는데 Segmentation Fault
