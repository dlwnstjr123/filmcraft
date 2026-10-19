# Windows 자동 자막 버전 빌드 (FilmCraft 포크)

이 포크의 첫 번째 목표는 기존 FilmCraft 음성 인식 기능을 활성화한 Windows 앱을 빌드하는 것입니다.

## 이번 변경 사항

- **기존 기능 사용**: `apps/filmcraft/Cargo.toml`에는 이미 `whisper` 기능이 정의되어 있습니다. 이 기능은 `filmcraft-engine/whisper`(음성 인식) 및 `filmcraft-engine/speech-download`(모델 다운로드)를 함께 켭니다.
- **별도 빌드**: `cargo build --release --locked -p filmcraft --features whisper`로 빌드합니다. `main`의 기본 설정은 건드리지 않습니다.
- **Windows 결과물**: GitHub Actions 실행이 **성공하면** `filmcraft.exe`가 Artifacts에 올라옵니다. GitHub Actions의 ZIP을 받아 압축을 풀어 실행하세요.

## GitHub에서 확인하는 방법

1. 저장소의 **Actions** 탭을 엽니다.
2. 포크에서 Actions가 꺼져 있으면, GitHub가 안내하는 **I understand my workflows, go ahead and enable them** 버튼을 눌러 활성화합니다.
3. 왼쪽의 **FilmCraft Windows - Whisper captions** 워크플로 실행 결과를 확인합니다. 이 브랜치에 새 커밋을 올리면 빌드가 시작되도록 설정되어 있습니다.
4. 초록색 성공 표시가 뜬 실행을 열고 아래 **Artifacts → filmcraft-windows-whisper** ZIP을 받습니다.
5. 압축을 풀고 `filmcraft.exe`를 실행합니다. 이 프로그램은 **서명되지 않은 개발용 빌드**이므로 Windows에서 경고할 수 있습니다. 자신이 빌드한 결과물인지 확인하세요.

## 자동 자막 사용 흐름

1. 영상/오디오를 불러와 시퀀스에 배치합니다.
2. **Text → Transcript** 패널에서 **Transcribe**를 사용합니다.
3. 생성된 transcript의 **Create captions** 버튼을 누르면 자막 트랙을 만들 수 있습니다.

현재 음성 인식 모델(Whisper 가중치)은 실행 파일에 포함되지 않습니다. **별도로 모델을 다운로드해야** 음성 인식이 작동합니다. FilmCraft의 엔진 명령은 `transcript.models`와 `transcript.downloadModel`이며 사용법은 [공식 transcripts 문서](transcripts.md)를 참조하세요. `whisper-base`는 다국어 모델이고 한국어 인식에 사용할 수 있습니다. 음성 인식에는 CPU 성능에 따라 시간이 걸릴 수 있습니다.

이 작업은 Android APK를 만들지 않습니다. 태블릿 지원은 별도 단계입니다.

## 검증 범위

워크플로는 Windows 빌드 성공 여부와 `filmcraft.exe` 파일 존재를 확인합니다. 실제 영상의 한국어 자동 자막 품질이나 자막 배치까지 자동 검증하지는 않습니다.
