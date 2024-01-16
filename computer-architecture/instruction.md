# 명령어

## 소스코드와 명령어

- **고급 언어** : 사람이 이해하고 작성하기 쉽게 만들어진 언어
  
  - **컴파일 언어** : 컴파일러에 의해 소스 코드 전체가 저급 언어로 변환되어 실행되는 언어
    
    - 목적 코드(object code) : 컴파일러를 통해 저급 언어로 변환된 코드
  
  - **인터프리터 언어** : 인터프리터에 의해 소스 코드가 한 줄씩 실행되는 언어

- **저급 언어** : 컴퓨터가 이해하고 실행할 수 있는 언어
  
  - **기계어** : 0과 1의 명령어 비트로 이루어진 언어
  
  - **어셈블리어** : 기계어를 읽기 편한 형태로 번역한 언어

## 명령어 구조

> 명령어 = 연산 코드 + operand

- **연산 코드(operation code)**
  
  - 명령어가 수행할 연산
  
  - 데이터 전송, 산술/논리 연산, 제어 흐름 변경, 입출력 제어로 분류됨
    
    <details>
    <summary>대표적인 연산 코드</summary>
    1. 데이터 전송 : MOVE, STORE, LOAD(FETCH), PUSH, POP <br>
    2. 산술/논리 연산 : ADD/SUBSTRACT/MULTIPLY/DIVIDE, INCREMENT/DECREMENT, AND/OR/NOT, COMPARE <br>
    3. 제어 흐름 변경 : JUMP, CONDITINOAL JUMP, HALT, CALL, RETURN <br>
    4. 입출력 제어 : READ(INPUT), WRITE(OUTPUT), START IO, TEST IO <br>
    </details>
    
    </details>
    
    </details>

- **오퍼랜드(operand, 주소 필드)**
  
  - 연산에 사용할 `데이터` 또는 연산에 사용할 데이터가 `저장된 위치`
  
  - 오퍼랜드의 수에 따라 0-주소 명령어, 1-주소 명령어, 2-주소 명령어, 3-주소 명령어라고 함

## 주소 지정 방식

- 유효 주소(effective address) : 연산 코드에 사용될 데이터가 저장된 위치

- 주소 지정 방식(addressing mode) : 연산에 사용할 데이터 위치를 찾는 방법

### 즉시 주소 지정 방식(immediate addressing mode)

- **연산에 사용할 데이터**를 operand에 직접 명시

- 가장 간단한 형태로 데이터를 찾는 과정이 없어 빠름

- 데이터의 크기가 작아짐

### 직접 주소 지정 방식(direct addressing mode)

- operand에 **유효 주소**를 직접 명시

- 표현 가능한 데이터의 크기는 즉시 주소 지정 방식보다 늘어남

- 표현 가능한 유효 주소의 크기가 연산 코드만큼 줄어듦

### 간접 주소 지정 방식(indirect addressing mode)

- **유효 주소의 주소**를 operand에 명시

- 두 번의 메모리 접근이 필요해 느림

### 레지스터 주소 지정 방식(register addressing mode)

- 연산에 사용할 데이터를 저장한 **레지스터**를 operand에 명시

- 레지스터 접근은 메모리 접근보다 빠름

- 표현 가능한 레지스터 크기가 제한됨

### 레지스터 간접 주소 지정 방식(register indirect addressing mode)

- 연산에 사용할 데이터를 메모리에 저장하고, **유효 주소를 저장한 레지스터**를 operand에 명시

- 메모리 접근 횟수가 한 번으로 줄어듦
