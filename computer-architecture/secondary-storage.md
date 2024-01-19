# 보조기억장치

# 하드디스크(HDD; Hard Disk Drive)

- 자기적인 방식으로 데이터 저장

- 구성 요소
  
  - 플래터(platter) : 데이터가 저장되는 원판
  
  - 스핀들(spindle) : 플래터를 회전시키는 구성 요소
  
  - RPM(Revolution Per Minute) : 분당 회전 수
  
  - 헤드(head) : 플래터의 데이터를 읽고 쓰는 구성 요소
  
  - 디스크 암(disk arm) : 헤드를 이동시키는 구성 요소

- 데이터 저장 단위
  
  - 트랙(track) : 플래터를 여러 동심원으로 나눈 것
  
  - 섹터(sector) : 트랙을 여러 조각으로 나눈 것
  
  - 블록(block) : 하나 이상의 섹터를 묶은 것
  
  - 실린더(cylinder) : 여러 겹의 플래터 상에서 같은 트랙이 위치한 곳을 모아 연결한 논리적 단위
    
    - 연속된 정보를 한 실린더에 저장해 헤드를 움직이지 않고 바로 읽을 수 있도록 함

- 데이터 접근 과정
  
  - 탐색 시간(seek time) : 접근하려는 데이터가 저장된 트랙까지 헤드를 이동시키는 시간
  
  - 회전 지연(rotational latency) : 헤드가 있는 곳으로 플래터를 회전시키는 시간
  
  - 전송 시간(transfer time) : 하드 디스크와 컴퓨터 간에 데이터를 전송하는 시간

## 플래시메모리(flash memory)

- 전기적인 방식으롣 데이터를 저장

- **NAND 플래시 메모리**와 NOR 플래시 메모리로 나눌 수 있음

- **셀(cell)** : 플래시 메모리에서 데이터를 저장하는 가장 작은 단위
  
  - 셀에 몇 비트를 저장할 수 있느냐에 따라 **SLC(Single Level Cell), MLC, TLC**, QLC로 나뉨
    
    - 한 셀에 n(n=1,2,3,4)비트의 정보를 저장할 수 있음
    
    - 한 셀에 2^n개의 정보를 표현할 수 있음
    
    - SLC로 갈수록 빠른 I/O 작업, 긴 수명을 가지나 비쌈

- 저장 단위
  
  - 셀(cell) -> 페이지(page) -> 블록(block) -> 플레인(plane) -> 다이(die)

- 플래시 메모리에서 **읽기/쓰기는 페이지** 단위로, **삭제는 블록** 단위로 이루어짐

- 페이지의 상태
  
  - **Free** : 어떠한 데이터도 저장하고 있지 않아 새로운 데이터를 저장할 수 있는 상태
  
  - **Valid** : 이미 유효한 데이터를 저장하고 있는 상태
  
  - **Invalid** : 유효하지 않은 데이터를 저장하고 있는 상태

- 가비지 컬렉션(garbage collection)
  
  - 유효하지 않은 쓰레기값을 정리하기 위한 기능
  1. 유효한 페이지만 새로운 블록으로 복사
  
  2. 기존 블록 삭제

## RAID(Redundant Array of Independent Disks)

> 데이터의 안정성과 높은 성능을 위해 여러 물리적 보조기억장치를 하나의 논리적 보조기억장치처럼 사용하는 기술

- RAID 0
  
  - 여러 보조기억장치에 데이터를 단순히 나누어 저장하는 구성 방식
    
    - stripe : 분산되어 저장된 데이터
    
    - striping : 데이터를 분산하여 저장하는 것
  
  - I/O 속도 형상
  
  - 안전하지 않음

- RAID 1
  
  - 복사본을 만들어 저장하는 방식(mirroring)
  
  - 백업과 복구가 쉬움
  
  - 쓰기 작업시 원본과 복사본을 두군데 저장하므로 느림
  
  - 사용 가능 용량이 적어저 비용이 증가함

- RAID 4
  
  - 오류를 검출하고 복구하기 위한 패리티 비트(parity bit)를 저장하는 장치를 따로 두는 구성 방식
  
  - 적은 용량으로 안전하게 보관 가능
  
  - 패리티 디스크의 병목 현상 발생

- RAID 5
  
  - 패리티 비트를 분산하여 저장하는 방식
  
  - RAID 4의 문제점인 병목 현상 제거

- RAID 6
  
  - RAID 5와 유사하나, 두 개의 패리티 비트를 두는 방식
  
  - RAID 4, RAID 5보다 안전하지만 느림