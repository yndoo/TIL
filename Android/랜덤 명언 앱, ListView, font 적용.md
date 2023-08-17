> 프로젝트 README.md 파일 완성하기 전 기록해두는 글입니다.  
> 나중에 보기 위해 리스트 뷰와 font 적용을 기록해두는 글입니다.



# 명언 애플리케이션
ListView를 사용한 랜덤 명언 애플리케이션을 개발하였다. 

## 완성 모습
애플리케이션 실행 시 랜덤 명언이 보이고, '전체 명언 보기' 버튼 클릭 시 모든 명언의 리스트가 보이는 모습이다.
![](https://velog.velcdn.com/images/kuronuma_daisy/post/4d3276fd-c15a-480a-843b-eb1630121530/image.gif)



#### MainActivity.kt
코드를 잘 보면 MainActivity와 SentenceActivity에서 같은 명언 리스트를 각각 새로 선언하여 사용한다.   

`sentenceList`라는 리스트를 하드코딩하였다. 그런데 이걸 똑같이 SentenceActivity에서도 하드코딩하여 사용했다! MainActivity에서 선언한 sentenceList를 활용해서 한 번만 선언하면 되는 구조로 바꾸고 싶어 intent.putExtra 종류를 활용해서 시도 중인데, 잘 안 되고 있다. 😭
```kotlin
package com.yndoo.goodwords

import android.content.Intent
import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import androidx.databinding.DataBindingUtil
import com.yndoo.goodwords.databinding.ActivityMainBinding

class MainActivity : AppCompatActivity() {

    private lateinit var binding:ActivityMainBinding

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val sentenceList = mutableListOf<String>()
        sentenceList.add("시간이 흐른다고 미래가 되지는 않는다.")
        sentenceList.add("먼 과거에 몰두하지 말고 가까운 현재를 파악하라.")
        sentenceList.add("인생에서 가장 진귀한 것은 시간이다.")
        sentenceList.add("결혼에는 많은 고통이 있지만 독신에는 아무런 즐거움이 없다.")
        sentenceList.add("야구에 만약이란 없습니다. 만약이란 걸 붙이면 다 우승하죠.")
        sentenceList.add("지식은 사랑이자, 빛이자, 통찰력이다.")

        binding = DataBindingUtil.setContentView(this, R.layout.activity_main)
        binding.showAllSentenceBtn.setOnClickListener {
            val intent = Intent(this, SentenceActivity::class.java)
            startActivity(intent)
        }

        binding.goodwordTextView.setText(sentenceList.random())
    }
}
```
#### SentenceActivity.kt
```kotlin
package com.yndoo.goodwords

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.ListView

class SentenceActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_sentence)

        val sentenceList = mutableListOf<String>()
        sentenceList.add("시간이 흐른다고 미래가 되지는 않는다.")
        sentenceList.add("먼 과거에 몰두하지 말고 가까운 현재를 파악하라.")
        sentenceList.add("인생에서 가장 진귀한 것은 시간이다.")
        sentenceList.add("결혼에는 많은 고통이 있지만 독신에는 아무런 즐거움이 없다.")
        sentenceList.add("야구에 만약이란 없습니다. 만약이란 걸 붙이면 다 우승하죠.")
        sentenceList.add("지식은 사랑이자, 빛이자, 통찰력이다.")

        val myadapter = ListViewAdapter(sentenceList)
        val listview = findViewById<ListView>(R.id.sentenceListView)

        listview.adapter = myadapter
    }
}
```

## ListView 기록

### 구조
![](https://velog.velcdn.com/images/kuronuma_daisy/post/95cef28b-e5a4-40ff-b8f7-1607d4beb253/image.png)  
개복치개발자님의 자료

1. SentenceActivity에서 데이터를 Adapter로 넘겨줌
2. Adapter에서 값을 하나씩 item으로 넘겨줌
3. item을 listview에 넣어줌

### SentenceActivity.kt
adapter에 데이터(sentenceList)를 넣어주고, listview에 adapter 등록(?)
```kotlin
        val myadapter = ListViewAdapter(sentenceList)
        val listview = findViewById<ListView>(R.id.sentenceListView)

        listview.adapter = myadapter
```
### ListViewAdapter.kt
adapter 코드!
```kotlin
package com.yndoo.goodwords

import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.BaseAdapter
import android.widget.TextView

class ListViewAdapter(val List: MutableList<String>): BaseAdapter() {
    override fun getCount(): Int {
        return List.size
    }

    override fun getItem(position: Int): Any {
        return List[position]
    }

    override fun getItemId(position: Int): Long {
        return position.toLong()
    }

    override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View {
        var convertView = convertView
        if(convertView==null){
            convertView = LayoutInflater.from(parent?.context).inflate(R.layout.listview_item, parent, false)
        }

        var listviewText = convertView?.findViewById<TextView>(R.id.listViewTextArea)
        listviewText!!.text = List[position]

        return convertView!!
    }
}
```
### listview_item.xml
리스트뷰에 들어가는 아이템에 대한 xml
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="60dp">
    <TextView
        android:id="@+id/listViewTextArea"
        android:text="TextArea"
        android:textSize="15sp"
        android:layout_margin="10dp"
        android:fontFamily="@font/bmjua_ttf"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"/>
</LinearLayout>
```

### activity_sentence.xml
리스트뷰가 있는 곳!
```xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout 
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    tools:context=".SentenceActivity">
    <ListView
        android:id="@+id/sentenceListView"
        android:layout_width="match_parent"
        android:layout_height="match_parent"/>
</androidx.constraintlayout.widget.ConstraintLayout>
```

## font 적용법

1. res 폴더 하위에 `font`폴더 생성
2. `ttf 파일`을 `font`폴더에 복사
![](https://velog.velcdn.com/images/kuronuma_daisy/post/58818864-4e1c-47bf-97d6-d584735e1ee4/image.png)
3. `android:fontFamily="@font/bmjua_ttf"` 로 설정하면 끝~
```xml
<TextView
     android:text="TextView"
     android:fontFamily="@font/bmjua_ttf"
     android:layout_width="wrap_content"
     android:layout_height="wrap_content"/>
```

## [깃허브](https://github.com/yndoo/GoodWordsApp)
