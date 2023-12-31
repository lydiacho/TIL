## 코인과 토큰

- 둘을 구분하는 기준 : `메인넷`의 유무

## ✔️ 코인

자체 `메인넷`을 보유, 독립된 생태계 구축

ex- 비트코인, 이더리움, 폴카닷, 에이다 …

- 참여자들이 메인넷을 유지/관리 by **채굴** → 이에 대한 보상으로 코인 지급
- 채굴 방식 : PoW, PoS …

### 블록체인 파생 방식

- `소프트 포크` : 기존 블록체인의 규칙을 가져가되, 조금 수정/추가
- `하드 포크` : 완전히 새로운 규칙을 세워 이전 블록체인과 호환되지 못함

→ 하드 포크하는 경우, 별도의 메인넷과 별도의 코인으로 보는 시각도 있음.

## ✔️ 토큰

독립적인 `메인넷`을 보유하지 않음

기존에 존재하는 메인넷 위에 **서비스/플랫폼**이 **특정 목적**을 위해 자신들만의 가상자산을 발행하는 경우

- 코인의 목적 : 메인넷 유지/관리
- 토큰의 목적 : 특정 서비스의 **유틸리티**

### 토큰 생성

**스마트컨트랙트**를 통해 토큰 **발행/분배/전송** 등의 작업을 자동화할 수 있다.

ex) ERC-20 : 가장 대표적인 이더리움 토큰의 표준

- **OpenZeppelin** 라이브러리를 통해 ERC-20 표준에 적합한 컨트랙트 개발 가능

### 토큰 종류

- `유틸리티 토큰` : 블록체인 기반 **서비스/앱 내**에서 특정 **목적**을 위해 쓰이는 토큰
  ex) 플랫폼 내에 여러 블록체인 게임 존재. 게임 내 재화를 특정 유틸리티 토큰으로 교환 가능
  → 플랫폼 내의 여러 게임들을 토큰을 통해 하나의 생태계로 묶어줄 수 있음
- `NFT`
- `STO`(토큰증권) : **기존 증권을 디지털화**해서 토큰 형태로 발행한 것
  - 온체인에 금융 데이터가 기록되는 새로운 전자증권 형태
  - 계약서 내용은 명백한 증권성을 띄기 때문에 다른 토큰들과 달리 **자본시장의 규제 체제 지배 하**에 있음
- `거버넌스 토큰` : 프로젝트 운영에 영향을 끼치는 **의사결정권**을 가지는 토큰
  - 토큰 보유 지분에 따라 커뮤니티에 끼칠 수 있는 영향력 부여
