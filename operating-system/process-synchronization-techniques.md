# 프로세스 동기화 기법

## 뮤텍스 락(Mutex lock; MUTual EXclusion lock)

- **상호 배제**를 위한 동기화 도구

- **자원이 하나**인 경우에만 사용 가능

- 자물쇠와 같은 역할

- 전역 변수 하나와 함수 두개로 구성됨
  
  - 전역 변수 `lock` : 프로세스가 공유하는 자물쇠 역할
    
    - 임계 구역의 자원 사용 여부
  
  - `acquire` 함수
    
    - 프로세스가 임계 구역에 진입하기 전에 호출
    
    - 임계 구역이 잠겨있다면 -> 임계 구역이 열릴 때까지(== lock이 false가 될 때까지) 임계 구역을 반복적으로 확인
      
      - 바쁜 대기 (busy waiting) : 자원을 사용할 수 있는지 계속 확인하는 것
    
    - 임계 구역이 열려있다면 -> 임계 구역을 잠그기(== lock을 true로 바꾸기)
  
  - `release` 함수
    
    - 임계 구역에서의 작업이 끝나고 호출
    
    - 현재 잠긴 임계 구역을 열기(==lock을 false로 바꾸기)
  
  ```java
  acquire() {
      while (lock == true) // 임계 구역이 잠겨있다면
          ;                // 임계 구역이 잠겨있는지 반복적으로 확인
      lock = true;         // 임계 구역이 잠겨있지않으면 임계 구역 잠금
  }
  
  release() {
      lock = false;       // 임계 구역 작업이 끝났으니 잠금 해제
  }
  
  acquire(); // 자물쇠 잠겨있는지 확인, 잠겨있지않으면 잠그고 들어가기
  /* 임계 구역에서의 작업 진행 */
  release(); // 자물쇠 반환  
  ```

## 세마포(semaphore)

- 뮤텍스 락과 비슷하지만 조금 더 일반화된 방식의 동기화 도구

- **공유 자원이 여러 개 있는 경우에도 적용 가능**

- binary semaphore, counting semaphore가 있는데 여기서는 **counting semaphore**를 지칭함
  
  - binary semaphore는 뮤텍스 락과 유사한 개념

- 임계 구역 앞에서 멈춤 신호를 받으면 잠시 기다리기다가 진입 가능 신호를 받으면 임계 구역 진입

- 전역 변수 하나와 함수 두 개로 구성됨
  
  - 전역 변수 `S`
    
    - 임계 구역에 진입할 수 있는 프로세스의 개수 == 사용 가능한 공유 자원의 개수
  
  - `wait` 함수
    
    - 임계 구역에 들어가도 좋은지, 기다려야할지 알려주는 함수
      
      - 바쁜 대기 (busy waiting) : 무한히 확인하는 것
  
  - `signal` 함수
    
    - 임계 구역 앞에서 기다리는 프로세스에게 진입 가능 신호를 주는 함수
  
  ```java
  wait() {
      while (S <= 0) // 임계 구역에 진입 가능한 프로세스의 개수가 0 이하라면
          ;          // 사용할 수 있는 자원이 있는지 반복적으로 확인
      S--;           // 임계 구역에 진입 가능한 프로세스의 개수가 1 이상이면 S를 1 감소시키고 임계 구역 진입
  }
  
  signal() {
      S++; // 임계 구역의 작업을 마친 뒤 S는 1 증가
  }
  
  wait();
  /* 임계 구역 */
  signal();
  ```

- **busy waiting 방지**를 위해 **프로세스의 상태**를 이용하고 불필요한 CPU 사이클 낭비를 방지
  
  - 사용 가능한 자원이 없는 경우 **대기 상태**로 만듦 (해당 프로세스의 PCB를 대기 큐에 삽입)
  
  - 사용 가능한 자원이 생기면 대기 큐의 프로세스를 **준비 상태**로 만듦 (해당 프로세스의 PCB를 대기 큐에서 꺼내 준비 큐에 삽입)
  
  ```java
  wait() {
      S--;
      if (S < 0) {
          add this process to Queue; // 해당 프로세스의 PCB를 대기 큐에 삽입
          sleep();                   // 대기 상태 진입
      }
  }
  
  signal() {
      S++;
      if (S <= 0) {
          remove a process p from Queue; // 대기 큐에 있는 프로세스 p를 제거
          wakeup(p);                     // 프로세스 p를 대기 상태에서 준비 상태로 만듦
      }
  }
  
  wait();
  /* 임계 구역 */
  signal();
  ```

- **실행 순서 동기화**를 위한 세마포
  
  - 세마포의 변수 **S를 0**으로 두고
  
  - 먼저 실행할 프로세스 **뒤에 signal 함수**를
  
  - 다음에 실행할 프로세스 **앞에 wait 함수**를

## 모니터(monitor)

- 세마포 사용 시 함수 호출을 누락하거나 실수한다면 오류 발생 => **모니터** 사용!

- **상호 배제**를 위한 동기화
  
  - 인터페이스를 위한 큐
  
  - 공유 자원에 접근하고자 하는 프로세스를 인터페이스를 위한 큐에 삽입
  
  - 큐에 삽입된 순서대로 한 번에 하나의 프로세스만 공유 자원 이용

- **실행 순서 제어**를 위한 동기화
  
  - **조건 변수(conditino variable)** 이용
    
    - 프로세스나 스레드의 실행 순서를 제어하기 위해 사용하는 특별한 변수
  
  - 각 조건 변수에 대한 큐를 이용해 실행 순서 제어
  
  - `조건변수.wait()` : 대기 상태로 변경, 조건 변수에 대한 큐에 삽입
  
  - `조건변수.signal()` : wait()로 대기 상태로 접어든 조건 변수를 실행 상태로 변경(== 준비 상태로 변경하는 함수)
  
  - 특정 프로세스가 아직 실행될 조건이 되지 않았다면 wait()를 통해 실행 중단
  
  - 특정 프로세스가 실행될 조건이 충족되었다면 signal()을 통해 실행 재개

- 모니터 안에는 하나의 조건 변수만 있을 수 있음
  
  - wait()를 호출했던 프로세스는 signal()을 호출한 프로세스가 모니터를 떠난 뒤에 수행 재개
  
  - signal()을 호출한 프로세스의 실행을 일시 중단하고 자신이 실행된 뒤 다시 signal()을 호출한 프로세스의 수행을 재개

- 자바의 `syncronized` 키워드

- 