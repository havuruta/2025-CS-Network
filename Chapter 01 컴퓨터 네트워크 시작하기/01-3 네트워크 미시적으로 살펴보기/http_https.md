### HTTP (HyperText Transfer Protocol)
- 웹 브라우저와 웹 서버 간의 데이터를 주고받는 프로토콜
- 데이터를 암호화하지 않고 평문(Plain Text)으로 전송 → 해킹(도청, 변조, 위장) 위험 있음
- 주로 보안이 크게 필요하지 않은 웹사이트에서 사용

### HTTPS (HyperText Transfer Protocol Secure)

- HTTP에 **SSL/TLS(암호화 보안 프로토콜)**을 추가하여 보안 강화
- 데이터를 암호화(Encryption)하여 전송 → 중간에서 가로채도 내용을 알 수 없음
- 인증서(Certificate)를 통해 서버의 신뢰성을 검증 (예: VeriSign, Let's Encrypt)
- 온라인 쇼핑, 금융 서비스, 로그인 등이 필요한 웹사이트에서 사용