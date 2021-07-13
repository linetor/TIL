#2021.07.13
## TIL
Spark dataframe 에서 map 타입의 column을 가지고 있다면, distinct 함수를 사용하지 못함
### 레퍼런스
https://stackoverflow.com/questions/55010434/spark-dataframe-select-distinct-rows/55011692
### 그래도 사용을 하려면
```
df.dropDuplicates("timestamp")
--> 
SELECT timestamp, first(c1) AS c1, first(c2) AS c2,  ..., first(cn) AS cn,
       first(canvasHashes) AS canvasHashes
FROM df GROUP BY timestamp
```
### 확인 결과
아직 확인이 안되었음 ^^;; --> 조금 애매하긴한데(join) 얼추 비슷해짐