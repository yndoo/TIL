## 1. drawable 폴더에 radius.xml 만들기
* 둥근 정도를 변경하고 싶으면 `<corners>`태그 내에서 Radius 속성들의 숫자를 변경해주면 된다.  
* 테두리 두께나 색상을 변경하고 싶으면 `<stroke>` 태그 내에서 속성을 변경하면 된다.  

`🔽radius.xml🔽`
```xml
<?xml version="1.0" encoding="utf-8"?>
<shape xmlns:android="http://schemas.android.com/apk/res/android"
    android:shape="rectangle" android:padding = "10dp">
    <solid android:color="#ffffff"></solid>
    <corners
        android:bottomLeftRadius="45dp"
        android:bottomRightRadius="45dp"
        android:topLeftRadius="45dp"
        android:topRightRadius="45dp"></corners>
    <stroke android:width="1dp"
        android:color="#BDBDBD"></stroke>
</shape>
```
![](https://velog.velcdn.com/images/kuronuma_daisy/post/5fa6eb01-519e-459f-b782-30253fab65bb/image.png)

해당 코드는 다음 블로그에서 참고하였다.  
https://coding-dahee.tistory.com/3

## 2. 적용하기
* 나는 RecyclerView의 item에 radius를 적용하고자 하였다.  
* 상단 `<LinearLayout>` 태그 내에서 backgroud 속성으로 "@drawable/radius"를 넣어주면 된다.  
`🔽rv_item.xml🔽`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="150dp"
    android:background="@drawable/radius"
    android:orientation="vertical">
    <ImageView
        android:src="@drawable/ic_launcher_background"
        android:layout_width="match_parent"
        android:layout_marginTop="10dp"
        android:layout_height="100dp"/>
    <TextView
        android:text="text"
        android:layout_gravity="center"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</LinearLayout>
```
아이템의 테두리가 둥글어진 모습이다.  
![](https://velog.velcdn.com/images/kuronuma_daisy/post/fdea69fd-3f17-443e-9257-09e69cfa6c18/image.png)
