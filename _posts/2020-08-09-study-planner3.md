---
layout: post
title: "스터디플래너 앱 개발일지(2)"
description: "8월 9일"
date: 2020-08-09
tags: [안드로이드, 개발, 개발일지]
comments: true
share: true
---


## 👉 오늘 한 일

### 1. 할일 완료 버튼 누르면 json에서 삭제

CustomAdapter 클래스에서 완료 버튼 이벤트에 ArrayList를 만들고, for로 저장되어 있는 json string을 파싱해 객체 별로 ArrayList에 넣어준다.
그 후에 **(json길이 - 완료 누른위치값)-1** 인덱스를 제거해주었다.
* recyclerview에 추가할때 최상단에 계속 쌓아서 position을 삭제하면 원하는 데이터가 삭제되지 않는다.
~~~
ArrayList<String> list = new ArrayList<String>();
                list.clear();
                int len = 0;
                try {
                    JSONArray jsonArray = new JSONArray(roadJson);
                    len = jsonArray.length();
                    if (jsonArray != null) {
                        for (int i=0;i<len;i++){
                            list.add(jsonArray.get(i).toString());
                        }
                    }
                } catch (JSONException e) {
                    e.printStackTrace();
                }
                list.remove((len-position)-1);
                roadJson = list.toString();
~~~


### 2. 수정된 데이터 기기에 저장하기

이렇게 수정된 데이터를 SharedPreferences에 저장해야 한다. 그래서 처음에는 이렇게 코드를 짰다.
~~~
SharedPreferences sharedPreferences = PreferenceManager
                .getDefaultSharedPreferences(context);
~~~
그러나 이렇게 하면 Adapter에서 저장한값과 MainActivity에서 호출하는 값은 이름이 같아도 따로 분리된다.
구글링해서 방법을 찾았다.
~~~
SharedPreferences sharedPreferences = context.getSharedPreferences(MyPREFERENCES, Activity.MODE_PRIVATE);
~~~
이렇게 MYPREFERENCES라는 고정된 string을 key값으로 sharedPreferences를 선언하면 같은 앱에서는 데이터를 공유하게 된다.
여기서 Acitvity.MODE_PRIVATE는 같은 앱에서 공유한다는 뜻이다.
찾아보니 이 파라미터를 바꾸면 다른 앱끼리도 데이터 쓰기/읽기가 가능하다고 한다.

### 3. DialogDatePicker 구현
할일추가 화면에 팝업으로 뜨는 날짜선택 창구현
~~~
datapickerBtn.setOnClickListener(new Button.OnClickListener() {
            @Override
            public void onClick(View view) {
                Calendar c = Calendar.getInstance();
                int mYear = c.get(Calendar.YEAR);
                int mMonth = c.get(Calendar.MONTH);
                int mDay = c.get(Calendar.DAY_OF_MONTH);


                DatePickerDialog dialog =
                        new DatePickerDialog(EditTodo.this, callbackMethod, mYear, mMonth, mDay);
                dialog.show();

            }
        });

~~~

날짜를 선택하면 yy-m-d 형식으로 변환한다. 그런데 이때 '월' 부분이 1씩 작게 나와서 1을 더해주었다.
서칭해보니 다른 사람들도 종종 발생하는 문제인 것 같다.
~~~
        callbackMethod = new DatePickerDialog.OnDateSetListener()
        {
            @Override
            public void onDateSet(DatePicker view, int year, int monthOfYear, int dayOfMonth)
            {
                datapickerBtn.setText((year+"-"+(monthOfYear+1)+ "-" + dayOfMonth));
            }
        };
~~~

> 이제 날짜별로 묶어서 데이터를 정리하는 걸 구현해야 한다. Gson이라는 라이브러리를 사용해야 할것 같기도 하다.
같은 field끼리 다시 리스트화해야 한다.

[수정] 코드를 바꾸어야 하긴 하지만, 아예 데이터를 만들때부터 날짜별로 push하면 되지 않을까?
