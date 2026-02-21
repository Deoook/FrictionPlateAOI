# FrictionPlateAOI

1. 광학계 구성
📸 카메라
4

25M 산업용 Area Scan Camera (Hikvision)

🔍 렌즈
4

16mm Lens

💡 조명
4

SMS Dome Light ( VCL-8DOM-WX 12V )

📐 광학 사양
항목	사양
FOV	약 200 × 200 mm
WD	290 mm
LWD	200 mm
Resolution	67.2 μm
2. 소프트웨어 구성
🛠 개발 환경

개발 언어 : C# WinForms

개발 툴 : Visual Studio 2019

라이브러리

OpenCV

자사 Vision Tool

SaigeVision (Deep Learning)

🧠 검사 알고리즘

자사 Tool을 이용하여
동 · 서 · 남 · 북 4방향 조명을 순차적으로 제어

총 4장의 이미지 취득

취득된 4장의 이미지를 기반으로
Albedo 이미지 생성

생성된 Albedo 이미지에 대해

X축 Gradient 영상 생성

Y축 Gradient 영상 생성

미분 영상을 통해

표면 형상 강조

결함 특징 강조

이후

Rule-based 검사 알고리즘

딥러닝 모델 (SaigeVision)

의 입력 데이터로 활용

3. Issue List
3.1 I/O 신호 문제

I/O 신호 인식 오류 발생

Bit 위치 및 Active Level 재정의 진행

3.2 Tact Time 개선
① 이미지 취득 방식 개선

Crop 기반 이미지 취득 방식 적용

구분	기존	개선
취득 시간	약 800 ms	약 600 ms
FPS	5 fps	6.5 fps
② 판정 로직 개선
구분	검사 Flow
기존	전면 촬영 → 프로세싱 → 결과 출력 → 후면 촬영 → 프로세싱 → 결과 출력
개선	전면 촬영 → 결과 출력 → 프로세싱 → 후면 촬영 → 프로세싱 → 결과 출력

딥러닝 처리 시간 기준
약 200 ms 단축

4. 검사 Sequence Flow
① Front 검사

Front Trigger 입력 (HIGH)

I/O BUSY 신호 → HIGH

Front 이미지 취득

Front 검사 및 프로세스 수행

② Front 검사 결과 처리

OK 신호 → HIGH

Complete 신호 → HIGH

③ Plate 뒤집기 동작 수행
④ Back 검사

Back Trigger 입력 (HIGH)

I/O BUSY 신호 → HIGH

Back 이미지 취득

Back 검사 및 프로세스 수행

⑤ 최종 판정

Front / Back 검사 결과 종합

OK / NG 판정 수행

⑥ 검사 완료 신호 출력

Complete 신호 출력

OK 또는 NG 신호 출력
