HAXM 설치가 자꾸 실패해서 Windows 기능에 있는 `Windows 하이퍼바이저 플랫폼` 기능을 체크하고 AVD를 사용했었다. 
![](https://velog.velcdn.com/images/kuronuma_daisy/post/e2f8211a-a2ab-4595-9d03-91b9cb3d8b3b/image.png)  
> HAXM 설치 실패하시는 분들 이 기능으로도 AVD를 사용할 수 있습니다!!

---
### HAXM 설치 정석(?) 해결 방법  
근데 다시 설치를 시도하던 중 어떤 스택오버플로우 선생님의 답변으로 해결되었다.
1. Windows 하이퍼바이저 플랫폼 기능을 모두 체크 해제
2. 전원 껐다 킴
3. SDK Tools에서 다시 설치 시도
-> 성공!!!!

[스택오버플로우 선생님의 답변 링크](https://stackoverflow.com/questions/16091677/intel-haxm-installation-error-this-computer-does-not-support-intel-virtualizat/27839301#27839301?newreg=083ced95cde1452e85fe1ed0431328bc)

사실 내 에뮬레이터가 화면 깜빡임이 심한 것이 haxm 설치를 실패했던 것과 연관이 있을까 해서 다시 설치 시도를 했던 것인데, 성공을 해도 화면 깜빡임은 사라지지 않았다...  

---
### 깜빡임 없이 화면 녹화하는 방법
![](https://velog.velcdn.com/images/kuronuma_daisy/post/bf5d557e-72bd-41ae-81f9-d5411a09a6f6/image.png)  
에뮬레이터 녹화에서 `Use emulator recording`을 체크 해제하고 녹화하면 화면 깜빡임 없이 녹화된다! (실행 시 내 눈에는 깜빡거리는게 보임)

* 트와이스 앱 녹화 gif
![](https://velog.velcdn.com/images/kuronuma_daisy/post/241e76a4-fb2d-4750-aa03-9dc869e7b495/image.gif)
