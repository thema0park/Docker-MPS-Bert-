# Docker-MPS-Bert-

## enviroment
DGX : Tesla V100 * 4
python : 3.7
tensorflow : 1.15

# Detail
## what is MPS?
- Multi-Process Service의 약자
- 다수의 프로세스가 동시에 단일 GPU에서 실행되도록 해주는 런타임 서비스.
- MPS 서버에 커널을 제출하는 방식.
  (공식 문서에서는 Server-client 방식을 사용)
-	서로 다른 컨텍스트의 커널들이 단일 컨텍스트로 인식되게 하여 디바이스의 리소스를 최대한 활용할 수 있게 해준다.

## Related Work
1. Stream
2. Hyper-Q

## Advantage
1. 공유 컨텍스트
  - 각 컨텍스트마다 할당되는 디바이스의 데이터 저장 공간이나 스케줄링 유닛 또한 공유될 수 있다는 것을 의미.
  - 컨텍스트 스위치 오버헤드가 줄어듬.
2. 자원 활용률이 향상되고 실행 시간의 감소를 기대할 수 있음.

## Limit
1. 다수의 MPS 클라이언트가 동시 실행되는 것과 달리, MPS서버는 오직 한 유저만이 실행시킬 수 있다.
  - 같은 UID로 서버에 제출된 클라이언트만 GPU에서 동시에 실행될 수 있다.
2. Dynamic parallelism은 지원되지 않는다
  - Dynamic parallelism이란?
3. Volta 이전의 디바이스에서는 어떻한 Stream Callback도 사용할 수 없다.
  - 따라서, 텐서플로우의 Stream Callback을 이용한 기능을 이용할 수 없을 수 있다.
4. MPS 클라이언트 중의 하나가 비정상적으로 종료된다면, MPS서버와 다른 클라이언트들이 어떤 상태에 있는지 알 수 없다.
