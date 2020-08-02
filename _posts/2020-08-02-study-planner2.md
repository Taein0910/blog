---
layout: post
title: "스터디플래너 앱 개발일지 08-02"
description: "8월 2일 개발일지"
date: 2020-07-26
tags: [안드로이드, 개발, 개발일지]
comments: true
share: true
---

## 오늘 구현한 것
- intent에서 값 전달받을 때 null 값 대응
~~~
 public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(data == null) {
            //데이터 전달 없이 액티비티 닫힘
            ...
        }
        }
~~~

- 타이머 누적 기능 구현
intent값 받으면 밀리세컨드초로 저장 후 date 함수로 HH:mm:ss 저장
https://stackoverflow.com/questions/9027317/how-to-convert-milliseconds-to-hhmmss-format

- json 저장
https://www.it-swarm.dev/ko/java/jsonarray%EB%A5%BC-%EB%AC%B8%EC%9E%90%EC%97%B4-%EB%B0%B0%EC%97%B4%EB%A1%9C-%EB%B3%80%ED%99%98/1072094561/

