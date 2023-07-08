나를 위한 기록

## Retrofit2 통신에 필요한 것
* 데이터 클래스
* Interface
* Retrofit.Builder 인스턴스

### 데이터 클래스
예시
```kotlin
data class Song(
    @SerializedName("singer")
    val singer: String,
    @SerializedName("album")
    val album: String,
    @SerializedName("title")
    val title: String,
    @SerializedName("duration")
    val duration: Int,
    @SerializedName("image")
    val image: String,
    @SerializedName("file")
    val file: String,
    @SerializedName("lyrics")
    val lyrics: String
)
```

### 인터페이스
GET 예시
```kotlin
interface RetrofitService {
    @GET("song.json")
    fun getSong(): Call<Song>
}
```
POST 예시
```kotlin
interface ApiService {
    @FormUrlEncoded
    @POST("testapi/first")
    fun postTest(
        @Field("age") age: String,
        @Field("name") name: String
    ): Call<TestInfo>
}
```
### Retrofit2 인스턴스
예시1
```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val retrofit = Retrofit.Builder().baseUrl("https://grepp-programmers-challenges.s3.ap-northeast-2.amazonaws.com/2020-flo/")
            .addConverterFactory(GsonConverterFactory.create()).build();
        val service = retrofit.create(RetrofitService::class.java)

        service.getSong().enqueue(object: Callback<Song> {
            override fun onResponse(call: Call<Song>, response: Response<Song>) {
                if (response.isSuccessful){
                    // 정상 통신
                    val result: Song? = response.body()
                    Log.d("성공", "내용 : "+ result.toString())
                } else {
                    // 통신 실패(응답코드 4XX 등)
                    Log.d("실패", "실패 ㅜ.ㅜ")
                }
            }

            override fun onFailure(call: Call<Song>, t: Throwable) {
                // 통신 실패(인터넷 끊김, 예외 발생 등 시스템적인 이유
            }
        })
    }
}
```
예시 2
```kotlin
btn.setOnClickListener { // 버튼 클릭시 실행
            if (inputText.text.toString().length!=0){ //공백이 아닐 때만
                val retrofit = Retrofit.Builder()
                    .baseUrl("https://33f2cc90-164b-4a35-8311-43dc926fb676.mock.pstmn.io/")
                    .addConverterFactory(GsonConverterFactory.create())
                    .build()

                val myserver: ApiService = retrofit.create(ApiService::class.java)

                myserver.postTest("200","amy").enqueue(object : Callback<TestInfo>{
                    override fun onFailure(call: Call<TestInfo>?, t: Throwable?) {
                        Log.e("retrofit T.T", t.toString())
                    }

                    override fun onResponse(call: Call<TestInfo>?, response: Response<TestInfo>?) {
                        Log.d("retrofit~!", response?.body().toString())
                    }
                })
            }
        }
```
#### 예시 1의 result.toString() 로그
![](https://velog.velcdn.com/images/kuronuma_daisy/post/fb921b06-bde4-4669-bb48-3ef0f3f0dcd0/image.png)
```
내용 : Song(singer=챔버오케스트라, album=캐롤 모음, title=We Wish You A Merry Christmas, duration=198, image=https://grepp-programmers-challenges.s3.ap-northeast-2.amazonaws.com/2020-flo/cover.jpg, file=https://grepp-programmers-challenges.s3.ap-northeast-2.amazonaws.com/2020-flo/music.mp3, lyrics=[00:16:200]we wish you a merry christmas
[00:18:300]we wish you a merry christmas
[00:21:100]we wish you a merry christmas
[00:23:600]and a happy new year
[00:26:300]we wish you a merry christmas
[00:28:700]we wish you a merry christmas
[00:31:400]we wish you a merry christmas
[00:33:600]and a happy new year
[00:36:500]good tidings we bring
[00:38:900]to you and your kin
[00:41:500]good tidings for christmas
[00:44:200]and a happy new year
[00:46:600]Oh, bring us some figgy pudding
[00:49:300]Oh, bring us some figgy pudding
[00:52:200]Oh, bring us some figgy pudding
[00:54:500]And bring it right here
[00:57:000]Good tidings we bring 
[00:59:700]to you and your kin
[01:02:100]Good tidings for Christmas 
[01:04:800]and a happy new year
[01:07:400]we wish you a merry christmas
[01:10:000]we wish you a merry christmas
[01:12:500]we wish you a merry christmas
[01:15:000]and a happy new year
[01:17:700]We won't go until we get some
[01:20:200]We won't go until we get some
[01:22:800]We won't go until we get some
[01:25:300]So bring some out here
[01:29:800]연주
[02:11:900]Good tidings we bring 
[02:14:000]to you and your kin
[02:16:500]good tidings for christmas
[02:19:400]and a happy new year
[02:22:000]we wish you a merry christmas
[02:24:400]we wish you a merry christmas
[02:27:000]we wish you a merry christmas
[02:29:600]and a happy new year
[02:32:200]Good tidings we bring 
[02:34:500]to you and your kin
[02:37:200]Good tidings for Christmas 
[02:40:000]and a happy new year
[02:42:400]Oh, bring us some figgy pudding
[02:45:000]Oh, bring us some figgy pudding
[02:47:600]Oh, bring us some figgy pudding
[02:50:200]And bring it right here
[02:52:600]we wish you a merry christmas
[02:55:300]we wish you a merry christmas
[02:57:900]we wish you a merry christmas
[03:00:500]and a happy new year)
```

### 참고
https://minchanyoun.tistory.com/44
