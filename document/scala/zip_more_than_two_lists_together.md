#2020.09.25
## TIL
두개 이상의 리스트를 튜플로 만들려고 할때
### 레퍼런스
https://stackoverflow.com/questions/1664439/can-i-zip-more-than-two-lists-together-in-scala
### 시용법
```
scala> (List(1,2,3),List(4,5,6),List(7,8,9)).zipped.toList
res0: List[(Int, Int, Int)] = List((1,4,7), (2,5,8), (3,6,9))
```
### 언제??
Spark 에서 groupBy로 묶을 때 collect_list로 하면 column이 다 따로 나옴. 이게 보기 힘드니까, 같이 묶어 놓으면 보기 편함.

근데 사용하기에는 이게 힘들수다 있다. 적당히 알아서 사용해야 됨