# Linking 1~12페이지 해석

## 1페이지

### 링킹

Woo Hyun Ahn (whahn@kw.ac.kr)

**그림 설명:** 강과 다리, 여러 척의 배가 보이는 풍경 그림을 배경으로 사용한 표지 페이지이다.

## 2페이지

### 목적 파일 형식

- 목적 파일의 내용
  - 파일 크기, 이진 코드 및 데이터 크기, 소스 파일 이름과 같은 목적 파일에 관한 일반 정보
  - 기계 아키텍처별 이진 명령어와 데이터
  - 심볼 테이블과 심볼 재배치 테이블
  - 디버그 정보
- 목적 파일 형식: 목적 파일 내용의 구성 방식
  - COFF(공통 목적 파일 형식)
  - ELF(실행 및 링킹 형식)
  - 기타
  - 파일 형식들은 서로 호환되지 않는다는 점에 유의하라.

## 3페이지

### 실행 및 링크 가능 형식(ELF)

- 목적 파일을 위한 표준 이진 형식
- AT&T System V Unix에서 유래함
  - 이후 BSD Unix 계열과 Linux가 채택함
- 다음을 위한 하나의 통합 형식
  - 재배치 가능 목적 파일(`.o`)
  - 실행 가능 목적 파일
  - 공유 목적 파일(`.so`)
- 일반 명칭: ELF 바이너리
- 이전의 `a.out` 형식보다 공유 라이브러리를 더 잘 지원함

## 4페이지

### 실행 및 링킹 형식(ELF)

- ELF 파일 형식에는 두 가지 서로 다른 해석 방식이 있다.
  - 링커는 섹션 헤더 테이블에 의해 기술되는 링크 가능한 모듈로 파일을 해석한다.
  - 로더는 프로그램 헤더 테이블에 의해 실행 가능한 모듈로 파일을 해석한다.

**그림 속 표기 해석**

- Linkable File: 링크 가능한 파일
- Executable File: 실행 가능 파일
- ELF Header: ELF 헤더
- Program Header Table (optional): 프로그램 헤더 테이블(선택 사항)
- Program Header Table: 프로그램 헤더 테이블
- Section 1 data / Section 2 data / Section n Data: 섹션 1 데이터 / 섹션 2 데이터 / 섹션 n 데이터
- Segment 1 data / Segment n Data: 세그먼트 1 데이터 / 세그먼트 n 데이터
- Section Header Table: 섹션 헤더 테이블
- Section Header Table (optional): 섹션 헤더 테이블(선택 사항)

**그림 설명:** 왼쪽은 링커가 ELF 파일을 섹션 단위로 해석하는 구조이고, 오른쪽은 로더가 실행 파일을 세그먼트 단위로 해석하는 구조이다. 링크 가능한 파일에서는 섹션 헤더 테이블이 중요하고, 실행 가능 파일에서는 프로그램 헤더 테이블이 중요하다.

## 5페이지

### ELF 형식 - 섹션

- 섹션
  - 목적 파일에서 시스템이 정의한 내용과 사용자가 정의한 내용은 내용의 유형 또는 특성에 따라 섹션이라고 불리는 단위로 묶인다.
- 섹션 유형
  - 코드
  - 초기화되지 않은 데이터(`bss`)와 초기화된 데이터
  - 정적 링킹을 위한 심볼 테이블
  - 문자열 테이블
  - 재배치 항목
  - 실행 시간 심볼 해시 테이블
  - 동적 링킹에 사용되는 정보
  - 동적 링킹을 위한 심볼 테이블

## 6페이지

### ELF 목적 파일 형식

- ELF 헤더
  - 매직 넘버, 유형(`.o`, 실행 파일, `.so`), 기계, 바이트 순서 등
- 프로그램 헤더 테이블
  - 페이지 크기, 메모리 세그먼트(섹션)의 가상 주소, 세그먼트 크기
- `.text` 섹션
  - 코드
- `.data` 섹션
  - 초기화된 정적 데이터
- `.bss` 섹션(Better Save Space)
  - 초기화되지 않은 정적 데이터
  - 초기화되지 않은 데이터는 목적 파일에서 실제 디스크 공간을 차지할 필요가 없다.

**그림 속 표기 해석**

- ELF header: ELF 헤더
- Program header table (required for executables): 프로그램 헤더 테이블(실행 파일에 필요)
- `.text` section: `.text` 섹션
- `.data` section: `.data` 섹션
- `.bss` section: `.bss` 섹션
- `.symtab`: 심볼 테이블
- `.rel.txt`: `.text` 재배치 정보
- `.rel.data`: `.data` 재배치 정보
- `.debug`: 디버그 정보
- Section header table (required for relocatables): 섹션 헤더 테이블(재배치 가능 파일에 필요)

**그림 설명:** ELF 목적 파일이 파일 오프셋 0의 ELF 헤더부터 시작하여 프로그램 헤더 테이블, 각 데이터 섹션, 심볼·재배치·디버그 정보, 섹션 헤더 테이블 순으로 구성되는 모습을 나타낸다.

## 7페이지

### ELF 목적 파일 형식(계속)

- `.symtab` 섹션
  - 심볼 테이블
  - 프로시저와 정적 변수 이름에 관한 정보
  - 섹션 이름과 위치
- `.rel.text` 섹션
  - `.text` 섹션을 위한 재배치 정보
  - 일반적으로 외부 함수를 호출하거나 전역 변수를 참조하는 모든 명령어
- `.rel.data` 섹션
  - 모듈이 참조하거나 정의하는 모든 전역 변수에 대한 재배치 정보
  - 일반적으로 초깃값이 전역 변수의 주소인 모든 초기화된 변수
  - 예: `int* p = &q;`
- `.debug` 섹션
  - 심볼릭 디버깅을 위한 정보(`gcc -g`)

**그림 설명:** 6페이지와 동일한 ELF 목적 파일 구조에서 `.symtab`, `.rel.text`, `.rel.data`, `.debug` 섹션이 어느 위치에 놓이는지를 보여 준다.

## 8페이지

### 정적 링킹

- 프로그램은 컴파일러 드라이버를 사용하여 번역되고 링크된다.

```text
unix> gcc -O2 -g -o myprog m.c a.c
unix> ./myprog
```

**그림 속 표기 해석**

- Source files: 소스 파일
- Translators (`cpp`, `cc1`, `as`): 번역기(`cpp`, `cc1`, `as`)
- Separately compiled relocatable object files: 개별적으로 컴파일된 재배치 가능 목적 파일
- Linker (`ld`): 링커(`ld`)
- Fully linked executable object file: 완전히 링크된 실행 가능 목적 파일
- contains code and data for all functions defined in `main.c` and `swap.c`: `main.c`와 `swap.c`에 정의된 모든 함수의 코드와 데이터를 포함함

**그림 설명:** `m.c`와 `a.c`가 각각 번역기를 거쳐 `m.o`와 `a.o`가 된 뒤, 링커 `ld`가 두 목적 파일을 결합하여 실행 파일 `p`를 만드는 과정을 나타낸다.

## 9페이지

### 정적 링킹

**그림 속 표기 해석**

- object file A / B / C: 목적 파일 A / B / C
- Text: 텍스트
- Data: 데이터
- bss: 초기화되지 않은 데이터
- Output: 출력

**그림 설명:** 목적 파일 A, B, C에 각각 들어 있는 `Text`, `Data`, `bss` 영역이 출력 파일의 같은 종류 영역으로 합쳐진다. 각 목적 파일의 코드들은 출력 파일의 `Text` 영역에, 초기화된 데이터는 `Data` 영역에, 초기화되지 않은 데이터는 `bss` 영역에 차례로 배치된다.

## 10페이지

### 예: 재배치 가능 목적 파일들을 실행 가능 목적 파일로 병합하기

`m.c`

```c
int e = 7;
int f = 10;

int main() {
  int g;
  int r = a();
  g = r * f;
  exit(0);
}
```

`a.c`

```c
extern int e;

int *ep = &e;
int x = 15;
int y;

int a() {
  return *ep + x + y;
}
```

**그림 설명:** 왼쪽에는 전역 변수 `e`, `f`와 `main()` 함수가 정의된 `m.c`가 있고, 오른쪽에는 외부 변수 `e`의 선언, 전역 변수 `ep`, `x`, `y`, 그리고 함수 `a()`가 정의된 `a.c`가 있다.

## 11페이지

### 재배치 가능 목적 파일들을 실행 가능 목적 파일로 병합하기

**그림 속 표기 해석**

- Relocatable Object Files: 재배치 가능 목적 파일
- Executable Object File: 실행 가능 목적 파일
- system code: 시스템 코드
- system data: 시스템 데이터
- more system code: 추가 시스템 코드
- headers: 헤더

**그림 설명:** 시스템 목적 파일, `m.o`, `a.o`에 분산되어 있던 섹션들이 하나의 실행 가능 목적 파일로 병합된다. 시스템 코드와 `main()`, `a()`는 `.text`에 들어간다. 시스템 데이터, `int e = 7`, `int *ep = &e`, `int x = 15`는 `.data`에 들어간다. 초기화되지 않은 `int y`는 `.bss`에 들어간다. `.symtab`과 `.debug` 정보는 파일 뒤쪽에 유지된다.

## 12페이지

### 실행 가능 바이너리 적재하기

**그림 속 표기 해석**

- Executable object file for example program `p`: 예제 프로그램 `p`의 실행 가능 목적 파일
- ELF header: ELF 헤더
- Program header table (required for executables): 프로그램 헤더 테이블(실행 파일에 필요)
- `.text` section: `.text` 섹션
- `.data` section: `.data` 섹션
- `.bss` section: `.bss` 섹션
- Section header table (required for relocatables): 섹션 헤더 테이블(재배치 가능 파일에 필요)
- Process image: 프로세스 이미지
- Virtual addr: 가상 주소
- init and shared lib segments: 초기화 및 공유 라이브러리 세그먼트
- `.text` segment (r/o): `.text` 세그먼트(읽기 전용)
- `.data` segment (initialized r/w): `.data` 세그먼트(초기화됨, 읽기/쓰기)
- `.bss` segment (uninitialized r/w): `.bss` 세그먼트(초기화되지 않음, 읽기/쓰기)

**그림 설명:** 실행 파일의 `.text`, `.data`, `.bss` 섹션이 메모리에 적재되어 프로세스 이미지의 대응 세그먼트가 되는 과정을 나타낸다. `.text`는 읽기 전용으로 적재되고, `.data`와 `.bss`는 읽기와 쓰기가 가능한 영역으로 적재된다. 오른쪽의 `0x080483e0`, `0x08048494`, `0x0804a010`, `0x0804a3b0`은 각 영역의 가상 주소를 나타낸다.
