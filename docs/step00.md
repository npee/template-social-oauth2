## Step 00 - 사전 준비
### 일반회원 로그인
ID와 password만 사용하는 간단한 Signin/Signup Controller를 만들어 테스트한다.
실제 데이터는 MySQL DB에 저장한다.
### REST API code 얻기
- Facebook  
https://developers.facebook.com
- Google  
https://console.cloud.google.com
- Kakao  
https://developers.kakao.com
- Naver  
https://developers.naver.com
- Github  
https://github.com/settings/developers
- ...

### https Local 환경 구성(SpringBoot)
Facebook의 경우에는 http에서 API 사용이 안되므로 https 환경을 만들어 주어야 한다.
1. 명령 프롬프트나 터미널에서 프로젝트 디렉토리로 이동한 후 다음 코드를 입력한다.
```$xslt
keytool -genkey -alias bns-ssl -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 3650
```
2. 다음 질문에 적절한 답을 해준 후 y로 마무리 하면 프로젝트 파일 목록에 `keystore.p12` 파일이 생성되어 있다.

```$xslt
키 저장소 비밀번호 입력:
새 비밀번호 다시 입력:
이름과 성을 입력하십시오.
  [Unknown]:  npee
조직 단위 이름을 입력하십시오.
  [Unknown]:  npee
구/군/시 이름을 입력하십시오?
  [Unknown]:
시/도 이름을 입력하십시오.
  [Unknown]:
이 조직의 두 자리 국가 코드를 입력하십시오.
  [Unknown]:  ko
CN=npee, OU=npee, O=npee, L=Unknown, ST=Unknown, C=ko이(가) 맞습니까?
  [아니오]:  y

```
3. `application.yml`에 다음 내용을 입력한다.
```$xslt
server:
  ssl:
    enabled: true
    key-store: keystore.p12
    key-store-password: {your-password}
    key-store-type: PKCS12
    key-alias: bns-ssl
  port: 8443
```
4. 아래 주소로 접근하여 *연결이 비공개로 설정되어 있지 않습니다* 라는 경고창이 뜨면 하단의 [고급] 버튼을 클릭하여 세부정보를 펼친 후 [localhost(안전하지 않음)으로 이동]을 클릭한다.
```$xslt
https://localhost:8443
```