# bestin-ha-config
Home Assistant Config files for Bestin IOT

## 사전 요구사항
- 스마트홈 2.0
- curl 명령어가 수행가능한 환경 (home assistant가 구동중인 서버)
- [jq](https://stedolan.github.io/jq/download/) 라이브러리 설치
  - 서버로부터 받은 json을 parsing 하기 위함
- 월패드 내 UUID 등록 작업 & 본인 거주 아파트의 CONTROL_URL
  - [개발자88님의 글 참고](https://cafe.naver.com/stsmarthome/38266)

## 설정 가이드
1. `shell_commands.yaml` 내 bestin_auth 명령의 인증 헤더에 있는 UUID에 앞서 월패드와 연동한 UUID 입력
2. `automations.yaml` 참고하여 주기적으로 bestin_auth command를 호출하여 인증토큰을 갱신하도록 자동화 구성
3. `rest_commands.yaml`, `sensors.yaml` 참고하여 URI를 본인 거주 아파트에 맞게 수정

## 기타
- repository 내 config들은 예시일 뿐이며, 참고하여 본인 아파트에 맞게 커스터마이징이 필요함.
- CONTROL_URL/v2/api/features/apply 통해 제어가능한 목록 확인 가능
- REST Client Tool등을 통해 직접 테스트 요청을 날려보며 작업하기를 권장함
- 난방(thermostat)의 경우, 테스트가 덜되었음
- API Interface의 기본 규격은 아래와 같음
  - 조회
    - GET / CONTROL_URL//v2/api/features/[feature명]/[방번호]/apply
  - 수정
    - PUT / CONTROL_URL/v2/api/features/[feature명]/[방번호]/apply
    ```json
    {
    "unit": "조회 통해 얻은 값",
    "state": "변경을 원하는 상태"
    }
    ```