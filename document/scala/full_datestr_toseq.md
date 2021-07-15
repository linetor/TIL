#2021.07.15
## TIL
spark 에서 원래 한달 통째로 데이터를 load 하려고 했는데, 데이터 사이즈가 커서 자꾸 메모리 문제랑 디스크 문제가 터져서 결국 하루 단위로 데이터를 로드 하는데, 하루단위로 된 달 전체를 만들기 애매해서 검색을 함.
### 레퍼런스
https://stackoverflow.com/questions/47157354/get-all-dates-as-list-for-given-month-and-year-in-scala
### 그래도 사용을 하려면
```
import java.util.Calendar
import java.text.SimpleDateFormat

val calendar = Calendar.getInstance
val formatter = new SimpleDateFormat("yyyy-MM-dd")

def allDaysForYear(year:Int, month:Int):List[String] = {
  calendar.set(year, month - 1, 1)

  (1 to calendar.getActualMaximum(Calendar.DAY_OF_MONTH)).map(_ => {
    val currentDate = calendar.getTime
    calendar.roll(Calendar.DATE, true)
    formatter.format(currentDate)
  }).toList
}
```
### 확인 결과
지금 열심히 돌아가고 있음. 아 resource 더 줄걸 ㅠㅠ 한 3일 넘게 걸리겠네 ㅠㅠ
## 추가 사항
Spark에서 데이터 로드 할때 데이터 위치에 ~~정규표현식~~  globe 라고 함(unix)
###
```
sqlContext.read
          .option("basePath","s3://bucket/location/")
          .format("orc")
          .load(s"""s3://bucket/location/da=202012??/""")
```
### 확인 결과
저렇게 하면 20201201 ~ 20201299까지 (아니네, 영어도 되니까 ㅠㅠ) \[0-9\] 이걸써야 했음