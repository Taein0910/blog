---
layout: post
title: "스터디플래너 앱 계획서"
description: "공부 계획 관리 앱 계획서"
date: 2020-07-26
tags: [안드로이드, 개발, 앱기획]
comments: true
share: true
---

## 주제 및 내용
스터디플래너 앱.
앱을 이용해 계획을 세워 효율적으로 공부할 수 있게 한다.

## 필요한 기능
-할 일 리스트
- 타이머
    - 타이머 내에 간단한 도구
- 요점 정리 보관함

## 기능 명세서
1) 할 일 리스트
- 메인화면에 표시
- 추가 버튼 클릭 -> 추가 액티비티 열기 -> 제목, 날짜, 목표 시간, (설명) 입력 -> 목록 추가
- 완료 체크 -> 목록에서 제거
- 리스트 클릭 -> 편집 화면
   - 편집화면 내 타이머 버튼 -> 타이머로 이동

2) 타이머
- 시작 되면 타이머 시작 -> 목표 시간 달성 시 진동
- 번역이나 계산기 등 학습에 필요한 도구 모음(webview로 제공?)
- 배경 검정색으로

3) 요점 정리 보관함
- 공부하면서 꼭 기억해야 할 것들 정리
- BottomNavigation Bar로 들어옴
- 추가 -> 액티비티 열기 -> 과목이나 카테고리 작성 -> 내용 입력(텍스트, (이미지)) -> 저장 -> 목록 추가
- 추가 액티비티에 삭제 버튼

![중간 이미지](https://i.imgur.com/baHnEef.png)

## 일정
- 1주 : 디자인 및 레이아웃 구성
- 2주 : TODO 리스트 구현
- 3주 : TODO 리스트 구현, 타이머 기능 구현
- 4주 : 타이머 부가 기능, 보관함 구현
- 5주 : 보관함 구현
- 6주 : 기타 기능 정리

## 필요한 기술 문서
- [기기에 데이터 저장 SharedPreferences](https://kylblog.tistory.com/7)


