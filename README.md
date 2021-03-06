# [2022년 2월] 이펙티브 코틀린

F-Lab 스터디 - 이펙티브 코틀린입니다.

## 팀원
- [theo](https://github.com/theo-f-lab)
- [이석균](https://github.com/Saerang)
- [김지원](https://github.com/jiwondev)
- [minseongkimdev(Castle)](https://github.com/minseongkimdev)
- [윤원준](https://github.com/gamzagamza)
- [김승태](https://github.com/soongjamm)
- [한태웅(hubert)](https://github.com/f-lab-hubert)
- [쿠키](https://github.com/hello-jiwon)

## 스터디 시간 및 장소
- 기간 : 2022년 2월 6일 ~ 2022년 3월 27일, 총 8주
- 시간 : 매주 일요일 오후 4시에서 ~ 6시
- 장소 : [F-Lab gather.town - 2번째 방에서 진행](https://gather.town/invite?token=qSwZpEnXEJVgA0x-AfVDJdspcCrAh3Zn)

## 스터디 방법
- 매주 1장씩을 읽어온다.
- 겹치지 않게 매주 2명을 선정하고, 2명은 책 내용을 정리한다.
- 스터디 당일에 랜덤으로 진행자를 뽑는다.
 - 스터디 당일 정리한 내용을 기준으로 이야기하고, 그 내용을 기준으로 추가하거나 제외할 내용을 다시 정리한다.
- 시끄러운 장소인 분들 만 마이크 OFF
- 매주 스터디 전 잡담 시간을 10분 정도 가진다.

## 랜덤으로 뽑기 위한 코드

```
fun main() {
    val list = mutableListOf("theo", "이석균", "김지원", "castle", "윤원준", "김승태", "한태웅", "쿠키")
    (1..3).forEach { _ ->
        val item = list.random()
        println(item)
        list.remove(item)
    }
}
```

## 스케줄

### 오리엔테이션
- 자기 소개
- 스터디장 선정 :[theo](https://github.com/theo-f-lab)
- 스터디 방식 선정

### 1주차 
- 1장에 대한 스터디 정리
  - [minseongkimdev(Castle)](https://github.com/minseongkimdev)
  - [saerang(이석균)](https://github.com/saerang)
- 발표자명 : 랜덤으로 뽑아서 진행

### 2주차
- 2장에 대한 스터디 정리
  - [김지원](https://github.com/jiwondev)
  - [김승태](https://github.com/soongjamm)

### 3주차
- 3장에 대한 스터디 정리
  - [윤원준](https://github.com/gamzagamza)
  - [한태웅(hubert)](https://github.com/f-lab-hubert)

### 4주차
- 4장에 대한 스터디 정리 - 추상화 설계
  - [theo](https://github.com/theo-f-lab)
  - [쿠키](https://github.com/hello-jiwon)

### 5주차
- 5장에 대한 스터디 정리 - 객체 생성
  - [이석균](https://github.com/Saerang)
  - [김지원](https://github.com/jiwondev)
