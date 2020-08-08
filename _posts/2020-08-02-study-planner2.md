---
layout: post
title: "스터디플래너 앱 개발일지(1)"
description: "8월 2일"
date: 2020-08-02
tags: [안드로이드, 개발, 개발일지]
comments: true
share: true
---


## 👉 오늘 한 일

### 1. intent에서 값 전달받을 때 null 값 대응

할 일 추가 액티비티와 타이머 액티비티에서 종료 버튼을 누르지 않고, 뒤로가기를 누르거나 아무런 값도 전달받지 못한 경우 mainAcitity에서 오류가 나며 죽어버렸다.
데이터를 전달받는 부분에서 data==null 값을 따로 처리해주어 해결했다.
~~~
 public void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
        if(data == null) {
            //데이터 전달 없이 액티비티 닫힘
            ...
        }
        }
~~~


### 2. 데이터 기기에 저장

원래는 firebase와 같은 서버와 연동하려 했으나 일단 사용자의 단말기에 저장하는 쪽으로 구현하기로 했다.
[sharePreferences](https://developer.android.com/reference/android/content/SharedPreferences)라는 라이브러리를 찾아서 사용했다. 사용법은 간단하다.
#### 데이터 저장하기
~~~
SharedPreferences.Edit editor = sharedPreference.edit();

editor.putInt(key값, 디폴트값);
editor.putLong(key값, 디폴트값);
editor.putBoolean(key값, 디폴트값);
editor.putString(key값, 디폴트값);
editor.putFloat(key값, 디폴트값);
editor.commit();
~~~
#### 데이터 가져오기
~~~
SharedPreferences.Edit editor = sharedPreference.edit();

editor.getInt(key값,디폴트값);
editor.getLong(key값,디폴트값);
editor.getBoolean(key값,디폴트값);
editor.getString(key값,디폴트값);
editor.getFloat(key값,디폴트값);
~~~


### 3. 타이머 누적 기능 구현

타이머를 사용해 학습시간을 기록하면 이 시간을 어떻게 누적할지 고민했다. 처음에는 타이머 액티비티에서 밀리세컨드를 전달받고 이를 시간 형식으로 전환하였다. 그리고 이 시간string을 sharePreference로 저장하는 방법으로 코드를 짰다. 그러나 같은 데이터를 여러번 변환해야 하는 번거로움이 있고, 무엇보다 다시 타이머 액티비티에서 값을 전달받을 때 코드가 복잡해진다. 그래서 타이머 액티비티에서 전달받은 **밀리세컨드를 sharePreference에 저장 -> 시간형식으로 변환해 표시**로 훨씬 간단하게 구현했다.

다음은 data함수를 이용해 밀리세컨드를 시간 형식(HH:mm:ss)로 변환하는 코드이다.
~~~
DateFormat formatter = new SimpleDateFormat("HH:mm:ss", Locale.KOREA); //형식 format 지정
        formatter.setTimeZone(TimeZone.getTimeZone("UTC"));
        String displayedTimer = formatter.format(new Date(Integer.parseInt(i))); //ms -> string 변환
~~~
[참고한 stackoverflow 답변](https://stackoverflow.com/questions/9027317/how-to-convert-milliseconds-to-hhmmss-format)


### 4. 할일 목록 어떻게 저장할까? --> json 저장
todo list의 목록을 recyclerview에 표시하고, 다음에 앱을 실행할 때도 기존 데이터를 로딩해 recyclerview에 그대로 표시해주어야 했다.
방법을 고민하던 중 json을 떠올리게 되었다.
**할일이 추가될 때 마다 json 데이터를 만들고 이를 sharePreferences에 저장 -> 다음에 실행할 때 json 파싱해 리스트화 한 후 recyclerview에 하나씩 추가**
#### 데이터 저장
~~~
final JSONObject object = new JSONObject();

                String name = data.getStringExtra("todotitle");
                String content = data.getStringExtra("content");
                String date = data.getStringExtra("date");
                //JSON데이터 생성

                try {
                    object.put("name", name);
                    object.put("content", content);
                    object.put("date", date);


                    jsonarrayTODO.put(object);
                    Log.e("data", jsonarrayTODO.toString());
                    SharedPreferences.Editor editor = sharedpreferences.edit();
                    editor.putString("todoJson", jsonarrayTODO.toString()); //투두 => json으로 저장
                    editor.apply();
                    } ...(생략)
~~~
#### 데이터 가져오기
~~~
String roadJSONTodo = sharedpreferences.getString("todoJson", ""); //기존 투두 데이터
        previousTodo = roadJSONTodo;
        try {
            JSONArray jsonarray = new JSONArray(roadJSONTodo);
            jsonarrayTODO = new JSONArray(previousTodo);
            for(int k=0; k < jsonarray.length(); k++) {
                JSONObject jsonobject = jsonarray.getJSONObject(k);
                String name       = jsonobject.getString("name");
                String content    = jsonobject.getString("content");
                String date  = jsonobject.getString("date");

                Todo todo = new Todo(name, "");
                mArrayList.add(0, todo); //RecyclerView의 첫 줄에 삽입
            }

        } catch (JSONException e) {
            Log.w("error", "something error!!", e);
        }
~~~
> JSONArray를 만들어줄때는 try/catch로 예외처리를 해주어야 한다. 안하면 오류가 발생했다.


### 5. todo리스트 일별로 표시해주기(준비)
[horizontal calendar](https://github.com/Mulham-Raee/Horizontal-Calendar)라는 라이브러리가 있어 사용했다.
![작은 이미지](https://github.com/Mulham-Raee/Horizontal-Calendar/raw/master/art/showCase.png)
☝ 요렇게 표시된다.

build.gradle(app)에 라이브러리를 추가해주어야 한다.
~~~
dependencies {
      implementation 'devs.mulham.horizontalcalendar:horizontalcalendar:1.3.4'
    }
~~~

xml에 이렇게 추가해주었다. 옵션을 지정해 색상을 커스텀해준다.
~~~
<devs.mulham.horizontalcalendar.HorizontalCalendarView
        android:id="@+id/calendarView"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginTop="10dp"
        android:background="@android:color/transparent"
        app:textColorSelected="#778beb"
        app:textColorNormal="#a9a9a9"
        app:selectorColor="#778beb"
        app:selectedDateBackground="#fff"/>
~~~

~~~
        Calendar startDate = Calendar.getInstance();
        startDate.add(Calendar.MONTH, -1);

        HorizontalCalendar horizontalCalendar = new HorizontalCalendar.Builder(this, R.id.calendarView)
                .startDate(startDate.getTime())
                .build();
~~~
이게 기본틀이고

~~~
horizontalCalendar.setCalendarListener(new HorizontalCalendarListener() {
            @Override
            public void onDateSelected(Date date, int position) {
                DateFormat formatter = new SimpleDateFormat("YYYY-M-d", Locale.KOREA);
                formatter.setTimeZone(TimeZone.getTimeZone("UTC"));
                Toast.makeText(MainActivity.this, formatter.format(date), Toast.LENGTH_SHORT).show();
            }
        });
~~~
⭐ 처음 선택되어 있는 날짜를 오늘날짜로 맞춰준다. ⭐


## 👉 오늘 한 것 중에서 고칠것
- [ ] 할일 데이터 제목외에도 설명, 날짜 파싱할 것
- [ ] 파싱한 데이터로 날짜별로 분류하고 horizontal calendar 선택에 따라 recyclerview 갱신해줄것
