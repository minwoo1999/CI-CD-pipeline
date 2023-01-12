# CI-CD-pipeline
CI/CD pipeline 
![image](https://user-images.githubusercontent.com/79193811/210244664-0ae8f217-7be6-4fd7-a1d6-296ab1cfc779.png)


### 1.GitHub access token 생성



### 2.GitHub 개인 레포지토리 webhook설정

* Payload URL - 젠킨스 서버 주소에 /github-webhook/ 경로를 추가하여 입력합니다.
* http://locahost:8080를 입력하시면 정상적으로 동작하지 않습니다.
* http://public-ip:8080 같이 공개 IP를 사용하는 경우에도 정상적으로 동작하지 않습니다.
* ngrok 어플리케이션을 통해 외부에서 접근할 수 있는 도메인을 사용합니다.
* Content type - application/json 타입을 사용합니다.

### 3. Gredentials 만들기

* 패스워드 영역에 GitHub 비밀번호가 아닌 액세스 토큰 정보를 입력합니다.
* GitHub 연결시 UserName과 Password로 만든 Credential만 사용 가능한 경우가 있습니다.
* Credential 관련 이슈 - https://github.com/jenkinsci/ghprb-plugin/issues/534


### 4.젠킨스 파이프라인 프로젝트 생성

* 파이프라인 설정Permalink 체크 박스를 선택합니다.
* GitHub project
* GitHub hook trigger for GITScm polling
* 아래 스크립트를 Pipeline 스크립트 영역에 붙여넣습니다. (Declarative 방식)
* Github에서 다운받을 브랜치와 레포지토리 정보를 입력합니다.
* 이전 단계에서 만든 github_access_token Credential을 추가합니다.

### 5. 파이프라인 생성에 성공하였으면 Build Now 버튼을 눌러 빌드를 실행합니다.

* docker push 중 denied: requested access to the resource is denied 다음과 같은오류가 발생하였다... 현재 ing 중
![image](https://user-images.githubusercontent.com/79193811/203500409-0bdedfdf-3cbc-4d48-837d-fcfe8b9ca035.png)

### 해결방안
* docker login -u "아이디" -p "비번!" docker.io 해당하는명령어를 입력해주면 정상적으로 작동 !
![image](https://user-images.githubusercontent.com/79193811/203733032-69d1058e-fb79-4f32-a05f-62de6f606aa2.png)

### docker run

![image](https://user-images.githubusercontent.com/79193811/211968813-5a54fd5d-1302-4d2a-89b2-b6078234d3f4.png)




### CI/CD WorkFlow Ver 1.0은 다음과 같습니다.

* 깃허브 main 브랜치에 변경사항 발생
* 깃허브가 웹훅을 Jenkins 서버에 전달
* Jenkins 서버는 main 브랜치를 pull 받아 gradle을 통해 test 및 build 명령 실행
* Gradle이 test 및 build 수행 후 Jar 파일 생성
* 생성된 Jar 파일을 Docker image로 build
* 생성된 Docker image를 Dockerhub로 전송
* Jenkins가 SSH를 통해 API 서버가 존재하는 EC2 Instance에 접속, SSH 상에서 Dockerhub를 통해 image를 pull
* 계속해서 SSH 상에서 Docker를 통해 컨테이너 실행

### Slack 연동하여 성공여부 확인

![image](https://user-images.githubusercontent.com/79193811/211968867-397d3785-6dda-4a78-890b-56a5a55e758f.png)



#### Reference site

* https://junhyunny.github.io/information/jenkins/github/jenkins-github-webhook/
* https://kanoos-stu.tistory.com/55
