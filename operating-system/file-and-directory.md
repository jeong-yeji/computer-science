# 파일과 디렉터리

- 파일 시스템(file system)
  
  - 파일과 디렉터리를 관리하는 OS 내의 프로그램
  
  - 파일과 디렉터리를 다루어주는 프로그램

## 파일 (file)

- 보조기억장치에 저장된 관련 정보의 집합

- 의미있고 관련있는 정보를 모은 논리적 단위

- **파일 구성 정보 = 실행 정보 + 부가정보(=속성, metadata)**

- 파일의 속성 : 유형(확장자, extension), 크기, 보호(권한), 생성일, 마지막 접근일, 마지막 수정일, 생성자, 소유자, 위치

- 파일 연산을 위한 시스템 호출 : 생성, 삭제, 열기, 닫기, 읽기, 쓰기 etc...

## 디렉터리 (directory)

- **트리 구조 디렉터리(tree-structured directory)**
  
  - 여러 계층으로 파일 및 폴더를 관리하는 구조
  
  - 최상위 디렉터리(루트 디렉터리, /), 서브 디렉터리
  
  - <> 1단계 디렉터리(single level directory) : 모든 파일이 하나의 디렉터리 밑에 있는 구조

- 경로(path)
  
  - 디렉터리를 이용해 파일과 디렉터리의 위치, 이름을 특정할 수 있는 정보
  
  - **절대 경로(absolute path)** : 루트 디렉터리를 기준으로 나타낸 경로
  
  - **상대 경로(relative path)** : 현재 디렉터리를 기준으로 나타낸 경로

- 디렉터리 연산을 위한 시스템 호출 : 생성, 삭제, 열기, 닫기, 읽기 etc...

- 파일 vs 디렉터리
  
  - 대부분 OS에서는 디렉터리를 **특별한 형태의 파일**로 간주함
  
  - 파일과 디렉터리를 크게 구분짓지 않음
  
  - 파일의 내부에는 파일과 관련된 정보, 디렉터리 내부에는 해당 디렉터리에 담긴 대상과 관련된 정보가 테이블(표) 형태로 구성 => **디렉터리 엔트리**

- **디렉터리 엔트리**
  
  - 디렉터리 테이블의 각 행
  
  - 디렉터리에 포함된 대상의 **이름** + 보조기억장치 내 파일이 **저장된 위치**(를 유추할 수 있는 정보)
