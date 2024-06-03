# Linux_homework
2022년 1학기 리눅스시스템프로그래밍 재수강 당시 제출했던 설계과제 목록

* (2023.10.07) P2_보고서.pdf 추가
* (2023.10.10) P2 ssu_sdup 파일 관련 Makefile 설명 추가
* (2023.10.14) P1_보고서.pdf 추가(실행 결과 및 날짜 캡처본 포함), Makefile 내 P2 ssu_sdup의 구현 여부 관련 설명 추가, Makefile 내 P1 ssu_find의 기능 및 구현 여부 관련 설명 추가
* (2024.06.03) P2 ssu_sdup 기본 기능 관련 설명 추가, 실행 사진 추가
---
## 목차
1. [설계과제1: ssu_sindex](#설계과제1-ssu_sindex)
2. [설계과제2: ssu_sdup](#설계과제2-ssu_sdup)
---
## 설계과제1 ssu_sindex
### ssu_sindex 개요: 파일 탐색 및 속성 비교 프로그램
* 지정된 파일 또는 디렉토리와 이름과 크기가 동일한 파일 및 디렉토리 검색
* 검색 결과 중 0번 인덱스의 파일과 서로 내용을 비교할 파일을 선택하여 두 파일의 내용 비교 결과를 출력
* 구현 실패했던 과제이나 설계과제1 구현 & 미구현 사항 식별 목적으로 관련 설명 기재

### ssu_sindex 파일 실행 방법
1. 리눅스 환경에서 P1 디렉토리째로 다운로드 후 실행
2. 리눅스 터미널 실행 후 현재 디렉토리를 P1로 이동
3. P1 디렉토리에서 다음의 명령어 입력(실행파일명: ssu_sindex)
#### 일반 디렉토리 혹은 그 내부 파일을 탐색할 경우
```
$ ./ssu_sindex
```
#### 시스템 디렉토리 혹은 그 내부 파일을 탐색할 경우
```
$ sudo ./ssu_index
```

### Makefile 실행 설명(./ssu_sindex를 통한 실행이 불가능한 경우)
* 리눅스 터미널을 통해 현재 디렉토리를 P1으로 이동 후 Makefile 실행
* ssu_sindex 실행파일이 P1 디렉토리 내부에 존재하지 않는 경우
```
$ make ssu_sindex
```
* 기존 오브젝트 파일 및 실행파일 삭제 후 다시 컴파일할 경우 아래 명령어를 순서대로 입력
```
$ make clear
$ make ssu_sindex
```

### ssu_sindex 기능 설명 및 사용법
#### [1. 도움말 출력 기능](필수기능, 구현)
* 명령어 사용법을 출력
```
학번> help
```

#### [2. 파일 탐색 및 비교 기능](필수기능, 미구현)
##### 기본 설명
* 프로그램 실행 후 내장명령어 find를 사용하여 이름과 크기가 같은 파일들의 정보를 리스트 형태로 출력
* 이름이 같은 파일이 디렉토리일 경우 디렉토리 내부에 저장된 파일 크기의 총합을 디렉토리의 크기로 취급

##### 파일 탐색(필수기능, 미구현)
```
학번> find 파일명 경로명
```
1. find: 이름과 크기가 같은 파일 탐색을 위한 명령어
2. 파일명: 탐색할 파일 및 디렉토리 이름
3. 경로명: 파일을 탐색할 디렉토리의 저장 경로
4. 검색 완료 후 아래 형식대로 명령어 입력
```
>> 인덱스번호 옵션
```
  5. 인덱스번호: 출력된 검색 결과 중 0번 인덱스의 파일과 비교할 파일의 인덱스 번호
  6. 옵션: 파일 및 디렉토리 비교 시 옵션

##### 일반 파일 내용상 차이점 출력(필수기능, 미구현)
* LCS 알고리즘을 응용하여 비교하고자 하는 두 파일의 내용을 행 단위로 대조 후 차이점 출력
  
##### 디렉토리 내용상 차이점 출력(필수기능, 미구현)
* 두 디렉토리의 하위 일반 파일 간 내용 혹은 하위 디렉토리 간 이름 비교 후 차이점 출력

#### [3. 프로그램 실행 종료 기능](필수기능, 구현)
```
학번> exit
```

### ssu_sindex 상세설명 및 실행결과 참조용 파일
* P1_보고서.pdf 파일 참조

---
## 설계과제2 ssu_sdup
### ssu_sdup 기본 기능 개요: 중복 파일 검색 프로그램
* 지정된 디렉토리 내부에서 지정된 확장자를 가진, md5 또는 sha1 해시값이 서로 동일한 중복 파일의 검색 결과 조회 및 삭제 기능 제공
* 파일명이 다르지만 서로 데이터가 동일한 파일들도 중복 파일로 취급하여 서로 다른 디렉토리에 저장된 동일한 데이터 파일의 저장 위치 조회 가능
* 데이터에 따른 해시값이 동일한 파일끼리 묶은 각각의 리스트는 파일 크기, 해시값, 저장 경로, 마지막 수정시간, 접근시간 순으로 정렬
* 각 데이터별로 크기, 해시값, 중복 파일의 저장 경로, 마지막 접근 및 수정 시간을 출력
* 리눅스 터미널에서 root 디렉토리 및 그 하위 디렉토리 탐색 가능(단, 검색할 확장자를 지정해야 사용 가능)
* 검색된 파일 중 지정한 파일 삭제 및 삭제 옵션 지정 가능
  
### ssu_sdup 파일 실행 방법
1. 리눅스 환경에서 P2 디렉토리째로 다운로드 후 실행
2. 리눅스 터미널 실행 후 현재 디렉토리를 P2로 이동
3. P2 디렉토리에서 다음의 명령어 입력(실행파일명: ssu_sdup)
#### 일반 디렉토리를 탐색할 경우
```
$ ./ssu_sdup
```
#### 시스템 디렉토리를 탐색할 경우
```
$ sudo ./ssu_sdup
```
(주의: 명령어를 입력하여 root 디렉토리부터 탐색할 경우, 검색할 파일의 확장자 또는 파일 크기 옵션을 별도로 지정해야 정상 동작)

### Makefile 실행 설명(./ssu_sdup을 이용한 실행이 불가능할 경우)
* 리눅스 터미널을 통해 현재 디렉토리를 P2로 이동 후 Makefile 실행
* ssu_sdup, fmd5, fsha1, help 중 1개라도 실행 파일이 존재하지 않는 경우
```
$ make all
```
* 기존 오브젝트 파일 및 실행 파일 삭제 후 다시 컴파일할 경우 아래 명령어를 순서대로 입력
```
$ make clean
$ make all
```

### ssu_sdup 기능 설명 및 사용법
#### [1. 도움말 출력 기능](필수기능, 구현)
```
학번>> help
```
1. help 또는 유효하지 않은 명령어 입력 시 ssu_sdup의 명령어 사용법 출력

   ![ssu_help](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/79e0d0cc-0dc6-458f-87cb-6c1843f26d6e)
  
#### [2. 디렉토리 내 중복 파일 검색 기능]
##### 기본 설명
* 중복 파일 리스트: 해시값이 동일한 파일끼리 모은 리스트
* 중복 파일 리스트 1개당 인덱스 개수는 최소 2개
* 디렉토리 내부에서 유일하게 존재하는 파일은 ssu_sdup의 검색 결과에서 제외
    
##### md5 해시값 기준 중복 파일 검색 기능(필수기능, 구현)
```
학번>> fmd5 확장자명 최소크기 최대크기 디렉토리명
```
1. fmd5: md5 해시값을 기준으로 동일한 파일끼리 묶어서 검색 결과 출력
2. 확장자명: * 입력 시 모든 파일 검색, *.(확장자) 입력 시 지정된 확장자를 갖는 파일만 검색(구현)
3. 최소크기 & 최대크기: 탐색할 파일의 크기 범위 지정, 크기범위 미지정 시 ~ 사용(구현)
4. 디렉토리명: 탐색을 수행할 디렉토리, 절대경로와 상대경로 모두 사용 가능(구현)

![ssu_find-md5_basic](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/afb04dac-6255-48cc-bc85-4623dda8f34f)


##### sha1 해시값 기준 중복 파일 검색 기능(필수기능, 구현)
```
학번>> fsha1 확장자명 최소크기 최대크기 디렉토리명
```
1. fsha1: sha1 해시값을 기준으로 동일한 파일끼리 묶어서 검색 결과 출력
2. 확장자명: * 입력 시 모든 파일 검색, *.(확장자) 입력 시 지정된 확장자를 갖는 파일만 검색(구현)
3. 최소크기 & 최대크기: 탐색할 파일의 크기 범위 지정, 크기범위 미지정 시 ~ 사용(구현)
4. 디렉토리명: 탐색을 수행할 디렉토리, 절대경로와 상대경로 모두 사용 가능(구현)

![ssu_find-sha1_basic](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/7f7844df-e813-4a98-a02d-f983865fc5d4)

#### [3. 탐색 결과 중 삭제할 파일 선택](필수기능 구현, 옵션 일부 미구현)
##### 기본 설명
* 중복 파일 검색 직후 출력되는 프롬프트에서 삭제할 파일 및 삭제 옵션 지정 가능

##### 삭제 파일 선택(필수기능 구현, 옵션 일부 미구현)
```
>> 파일묶음번호 삭제옵션 [인덱스번호]
```
1. 파일묶음번호: 삭제하고자 하는 파일에 해당하는 리스트의 번호 선택(필수기능, 구현)
2. 삭제옵션
   * d: 선택한 리스트 내 지정된 인덱스에 해당하는 중복 파일 삭제(필수기능, 구현)
  
     ![ssu_find-md5-doption](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/e1b3d4b3-292a-4e07-8d53-4311637cfde3)
     ![ssu_find-sha1-doption](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/14a5c223-49a2-44a1-a7c8-572564296cd5)

   * i: 선택한 리스트 내 각 중복 파일마다 삭제 여부 확인 메시지를 출력하여 삭제 여부 확인(선택기능, 미구현-출력오류)
   * f: 선택된 리스트 내 파일 중 가장 최근에 수정된 파일을 제외한 나머지 중복 파일 삭제 후 선택된 리스트만 제외된 검색결과 다시 출력(선택기능, 구현)
  
     ![ssu_foption](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/213e9cd7-7b41-4a52-9da7-c018228ad2b1)
     ![ssu_find-sha1-foption](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/743c8688-a7dd-4522-98a0-60ce5ecf16b9)

   * t: 선택된 리스트 내 파일 중 가장 최근에 수정된 파일을 제외한 나머지 중복 파일을 휴지통으로 이동(필수기능, 구현)

     
     ![ssu_find-sha1_toption](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/1851f31e-a810-4f39-9a94-dadf52540a1b)


3. 인덱스번호: d옵션 선택 시에만 추가 입력 가능, 추가 입력 가능 한 리스트 내 해당 인덱스의 파일을 삭제(필수기능, 구현)

##### 삭제 파일 선택 종료(필수기능, 구현)
```
>> exit
```

#### [4. 프로그램 실행 종료 기능](필수기능, 구현)
```
학번>> exit
```
![ssu_exit](https://github.com/HyeonBin2379/Linux_homework/assets/53569820/bfa06251-9f73-4669-8174-124e130375c4)

### P2 ssu_sdup 관련 상세설명 및 실행 결과 확인 
* P2_보고서.pdf 파일 참조
