# CI-CD-pipeline
CI/CD pipeline 
![image](https://user-images.githubusercontent.com/79193811/203499552-8bca4bd2-36b4-4d81-88f8-f7233e1a6604.png)

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


#### Reference site

* https://junhyunny.github.io/information/jenkins/github/jenkins-github-webhook/
* https://kanoos-stu.tistory.com/55
