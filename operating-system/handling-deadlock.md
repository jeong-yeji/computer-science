# 교착 상태 해결 방법

## 교착 상태 예방

- 교착 상태가 발생하지 않도록 교착 상태 발생 조건 중 하나를 없애버리기

- 교착 상태가 발생하지 않음은 보장하나 부작용이 따름

- **상호 배제 제거**
  
  - 모든 자원을 공유하게 만든다
  
  - 현실적으로 **불가능**함

- **점유와 대기 제거**
  
  - 특정 프로세스에게 자원을 모두 할당하거나, 아예 할당하지 않는 방식으로 배분
  
  - 한 프로세스에 필요한 자원을 몰아주는 방식
  
  - **자원의 활용률이 떨어짐**
  
  - 많은 자원을 사용하는 프로세스는 계속 대기하면서 기아 현상 발생 가능

- **비선점 제거**
  
  - 선점 가능한 자원(e.g. CPU)에 한해 효과적
  
  - **선점이 불가능한 자원**도 있음

- **원형 대기 제거**
  
  - 모든 **자원에 번호**를 붙이고 번호의 **오름차순대로 할당**하면 원형 대기는 발생하지 않음
  
  - 가장 현실적이고 실용적임
  
  - 모든 자원에 번호를 붙이는 것은 어려운 작업
  
  - 어떤 자원에 어떤 번호를 붙이느냐에 따라 자원의 활용률이 달라짐

## 교착 상태 회피

- 교착 상태를 **무분별한 자원 할당**으로 인해 발생했다고 간주

- **배분 가능한 자원의 양을 고려**해 교착 상태가 발생하지 않을만큼만 자원 배분

- **항상 안전 상태를 유지**하도록 자원을 할당하는 방식

- 은행원 알고리즘

- **안전 순서열(safe sequence)**
  
  - 교착 상태없이 안전하게 모든 프로세스에 자원을 할당할 수 있는 순서

- **안전 상태(safe state)**
  
  - 교착 상태없이 모든 프로세스가 자원을 할당받고 종료될 수 있는 상태
  
  - 안전 순서열이 있는 상태

- **불안전 상태(unsafe state)**
  
  - 교착 상태가 발생할 수도 있는 상태
  
  - 안전 순서열이 없는 상태  

## 교착 상태 검출 후 회복

- 교착 상태가 발생 후 조치하는 방식

- 프로세스가 자원을 요구하면 일단 할당하고 교착 상태가 검출되면 회복

- **선점을 통한 회복**
  
  - 교착 상태가 해결될 때까지 한 프로세스씩 자원을 몰아주는 방식

- **프로세스 강제 종료를 통한 회복**
  
  - 교착 상태에 놓인 프로세스 **모두 강제 종료** -> 작업 내역을 잃을 수 있음
  
  - 교착 상태가 해결될 때까지 **한 프로세스씩 강제 종료** -> 오버헤드(교착 상태가 없어졌는지 매번 확인해야됨)

## ~~교착 상태 무시~~

- ~~교착 상태가 드물게 발생한다면 적용 가능...~~

- ~~타조 알고리즘~~