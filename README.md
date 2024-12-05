# 실행 전 알아야 하는 사실
- front-end 코드는 visual studio code로 실행하여, npm install, npm start를 합니다.
- back-end 코드는 openAI api를 결제 후 사용하는 것이기 때문에 보안에 신경을 썼습니다.
- 따라서 Eclipse로 실행을 할 경우, Run Configurations -> 좌측에서 VM 옵션을 추가할 실행 구성(예: Java Application)을 선택 -> 우측 탭에서 Arguments 선택 -> VM arguments 섹션에 (비밀번호)를 입력합니다.
- IntelliJ로 실행을 할 경우, Run 오른쪽에 있는 메뉴 클릭 -> Configuration -> Edit -> Modify options -> Add VMoptions -> 빈칸에 (비밀번호) 을 입력합니다.
- 또한, 실행 후 첫 페이지인 localhost:5173은 시크릿 창으로 열면 됩니다.

# 🎮 AI기반 이미지 추측 게임 EMOJINIOUS

![logo](/image/1.png)

# 📃 프로젝트 소개 및 개발배경

- 이모지니어스는 AI 기술과 프롬프트 엔지니어링을 게임과 이모지 형식의 캐릭터들을 통해 친숙하게 경험할 수 있도록 개발된 플랫폼입니다.

- 이 프로젝트는 AI와의 상호작용을 자연스럽게 유도하며, 사용자들의 AI 리터러시와 프롬프트 엔지니어링 능력을 향상시키는 것을 목표로 합니다.

- 현대 사회에서 AI 기술은 빠르게 확산되고 있으며, 일상생활에서 그 중요성이 점점 커지고 있으나, AI에 익숙하지 않은 사람들에게는 여전히 복잡하고 이해하기 어려운 분야로 느껴집니다. 이모지니어스는 이러한 장벽을 허물고자, 누구나 쉽게 접근할 수 있는 게임 형식을 통해 AI와의 상호작용을 촉직할 수 있도록 설계되었습니다.

# ⚙️ 개발 환경

- Frontend(React 18.2.0, Vite)
  - Deployment: Vercel
  - Communication: SockJS, STOMP
- Backend(Java 17, Spring Boot 3.3.2, Gradle) - Infrastructure: AWS EC2
  - Data Management: Redis
  - Communication: REST API, WebSocket
  - AI Services: OpenAI(DALL-E3, GPT-4) API
- Scoring Server(Python 3.12.3, FastAPI, Uvicorn)
  - HW & OS: Raspberry Pi 5, Ubuntu Server 24.04 LTS - AI/ML: PyTorch, BERT(bert-kor-base)
- Tools
  - IDEs: IntelliJ IDEA, Visual Studio Code

# 🛠️ 시스템 아키텍처

![frame](/image/2.png)

# ⛳️ 페이지별 기능

### [시작화면]

- 게임시작 시 캐릭터 선택 및 닉네임 입력 페이지가 나타납니다.

![start](/image/3.png)

### [캐릭터 선택 및 닉네임 입력]

- 총 10개의 캐릭터가 있으며, 화살표를 클릭하여 캐릭터를 차례로 볼 수 있습니다. 

![charactor](/image/4.png)

### [메인 화면에서의 게스트 초대]

- 방장이 처음 방에 들어가게 되면 나오는 화면입니다.
  - 방장은 초대 버튼을 눌러 사용자들을 초대할 수 있는 링크를 복사할 수 있습니다.
  - 링크는 각각의 방을 구별할 수 있도록, 각각의 session id가 파라미터로 붙은 형식입니다.
  - 게스트가 링크를 통해 입장하게 되면, 캐릭터 선택 및 닉네임 입력을 할 수 있는 페이지가 나오며, 모두 입력한 뒤에는 초대자의 방으로 입장하게 됩니다.

![invite](/image/5.png)

### [메인 화면]

- 게임은 방장 포함 두 명 이상이 되어야 실행할 수 있습니다.

- 게임 설정 및 채팅이 가능합니다.
  - 게임 설정에는 주제, 난이도, 턴, 프롬프트 입력시간, 정답 입력시간이 포함됩니다. 
  - 설정이나 채팅이 업데이트 되었을 시에는 업데이트 된 부분에 알림이 뜨며, 업데이트 된 사실을 바로 알 수 있습니다.   

![main](/image/6.png)

![mainSetting](/image/7.png)

### [프롬프트 입력]

- 게임이 시작되면 주제에 맞는 키워드를 AI가 생성하여 각각의 플레이어에게 던져줍니다.

- 이후 플레이어들은 그에 맞는 설명을 시간 안에 입력합니다.

- 입력창 아래에는 타이머가 존재하며, 몇 명이 프롬프트를 제출하였는지 확인할 수 있습니다. 

![prompt](/image/8.png)

### [이미지 생성 페이지]

- AI가 프롬프트 입력을 기반으로 이미지를 생성하는 동안 로딩 페이지가 띄어집니다.

![image](/image/9.png)

### [자신의 이미지 확인 및 상대의 이미지 추측]

- 이미지가 생성되면 각각의 플레이어는 자신의 이미지를 먼저 확인합니다.

- 자신의 이미지를 확인한 뒤에는 다른 플레이어의 이미지를 연달아 추측합니다.

![myImage](/image/10.png)

![other1](/image/11.png)

![other2](/image/12.png)

### [점수 계산 페이지]

- 모두의 추측이 끝나면 점수 계산 로딩 페이지로 이동합니다.

![calcul](/image/13.png)

### [최종 결과]

- 점수 계산이 끝나면 결과가 나타나게 됩니다.

![final](/image/14.png)

### [보완하고 싶은점]

- 게임이 끝나고 최종 결과가 나왔을 때, 한번더 플레이와 메인화면으로 돌아가기 등의 기능이 있었으면 좋았을 것 같다.
- 최종 결과를 등수별로 나열하는 방식이 결과를 확인하는데 더 좋았을 것 같다.

# ⭐️ 기타

- 키워드 제공 방식
  - GPT-4 모델을 사용하여 테마와 난이도에 따른 한국어 키워드셋을 생성합니다. 생성된 키워드셋은 Redis 캐시에 저장되며, 일주일 동안 유지됩니다. 캐시된 키워드셋이 있을 경우 새로 생성하지 않고 기존 키워드셋을 사용합니다.
- 이미지 생성 방식
  - DALL-E 3 모델을 사용하여 생성됩니다. 사용자가 제출한 프롬프트를 게임 설정에 따라 정제/변조 후 사용합니다. 생성된 이미지는 1024x1024 픽셀 크 기의 단일 이미지로, 별도의 저장은 하지 않습니다. 생성된 이미지는 일시적 으로 유효한 URL 형태로 제공됩니다.
- 점수 산정 방식
  - kykim/bert-kor-base 모델을 사용하여 정답과 제출한 답의 CLS 토큰 임베 딩 간 코사인 유사도를 계산하고, 이를 백분율로 변환한 후 로그 스케일링 을 적용하여 최종 점수를 산출합니다.
  - score = ((base^similarity_percentage - 1) / (base^100 - 1)) * 100, where base = 1.2
  - 정답을 맞춰서 얻은 점수의 70%를 그림의 주인도 얻게 됩니다. 따라서 다른 사람의 그림을 잘 맞추는 것도 중요하지만, 다른 플레이어들이 내 그림을 맞출 수 있도록 잘 설명하는 것도 중요합니다.

# Reference, License
- 디자인은 시각디자인학과 학우의 도움을 받았습니다.
- This project is licensed under the BSD License


