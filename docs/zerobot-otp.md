# Zerobot OTP

제로페이지 슬랙에 있는 사용자를 입증할수 있는 일회용 비밀번호(OTP)를 발급하는 기능

## zerobot otp 인증 Flow
1. User가 Slack에서 ```zerobot otp```를 입력하여 OTP 를 발급한다.
2. Zerobot은 OTP를 해당 유져의 DM으로 전송한다.
3. 인증을 원하는 곳(앱, 다른 Thrid party, 이하 App)에서 유져 이름과 해당 OTP를 입력 받는다.
4. App에서 다음과 같은 정보로 http 요청을 한다.
	* url : https://zerobot.herokuapp.com/hubot/otp/:name
	* method : POST
	* param
		* name : 유져 이름
	* body :
		* token : OTP
5. http 응답으로 vaild 여부를 판단한다.
	* token이 vaild한 경우 : http response code 200
	* token이 vaild하지 않은 경우 : http response code 401

request example with curl

```
curl -X POST -v -d token=006276 https://zerobot.herokuapp.com/hubot/otp/bluemir
```

**주의! OTP는 30초만 유효하므로 매번 vaild요청을 보내면 인증에 실패합니다.**
인증시 한번만 사용하고 인증이 완료된 사실은 각 App서 별도로 기억해야만 합니다.
