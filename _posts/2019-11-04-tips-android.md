---
layout: post
title: "[TIP] Android"
categories:
  - Tips
tags:
  - tips
  - android
  - xml
  - layout

last_modified_at: 2019-11-04T
---

###### INDEX
* [LinearLayout에서 양쪽으로 정렬하고 싶을 때!](#tip-1)

<br>

---
###### tip 1
## LinearLayout에서 양쪽으로 정렬하고 싶을 때!

정렬하고자 하는 뷰 사이에 가로, 세로 0dp 에 weight 가 1인 View를 하나 넣으면 끝!

```xml
<TextView
    android:layout_width="wrap_content"
    android:layout_height="match_parent"
    android:gravity="center"
    android:text="정보"
    android:textSize="18dp"
    android:textStyle="bold"
    android:textColor="#000000"/>

<View
    android:layout_width="0dp"
    android:layout_height="0dp"
    android:layout_weight="1" />

<ImageButton
    android:id="@+id/post"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:src="@drawable/ic_edit"
    android:scaleType="centerInside"
    android:background="@color/colorPrimaryLight"
    android:layout_gravity="right"/>
```

---
