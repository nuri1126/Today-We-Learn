# 효율적인 쿼리
> 19-04-02 <a href="https://github.com/jinnyy">@jinnyy</a>

다른 문서를 참고해 효율적인 쿼리문 작성법을 정리해보았습니다.


<br><br><br>

1. WHERE문에서 `AND`를 사용할 때에는 가장 제한적인 조건을 앞에 쓰자
    - 더 적은 row에 해당되는 조건을 앞에 쓰면 더 빠르게 동작합니다.
    - = 연산이 부등호 연산보다 빠를 수도 있고... 등등

<br>

2. `OR`로 조건을 지정한다면 가장 덜 제한적인 조건을 앞에 쓰자
    - OR은 true이면 뒤의 조건을 고려하지 않는다는 점에서, 
    더 많은 row가 해당되는 조건을 앞에 쓰면 뒤에 나오는 조건을 체크하지 않아도 되므로 더 빠른 속도를 낼 수 있습니다.

<br>

3. `<>`(NOT) 대신 조건문으로 풀어쓰자
    - <>연산을 수행하기 위해 전체 테이블을 읽게 됩니다. 따라서 연산 속도가 느려집니다.
    ```SQL
    SELECT * FROM student WHERE gpa<>3.5
    ```
    대신
    ```SQL
    SELECT * FROM student WHERE gpa < 3.5 OR gpa > 3.5
    ```

<br>  
  
4. `IN`절을 사용할 때에는 가장 확률이 높은 비교치에서부터 가장 낮은 비교치로 순서를 지정하자
    ```SQL
    SELECT * FROM student WHERE UPPER(last) IN ("SMITH", "PETERSON")
    ```
   대신
    ```SQL
    SELECT * FROM student WHERE UPPER(last) IN ("PETERSON", "SMITH")
    ```

<br>

5. `LIKE`절 자체로는 최적화되지 않는다.
    - 와일드카드를 포함한 LIKE절은 (서버가 자체적으로) 최적화하기 어려우므로 다른 방법을 시도해보는 것이 좋습니다.
    ```SQL
    SELECT * FROM student WHERE upper(last) LIKE "SM_TH"
    ```
   대신
    ```SQL
    SELECT * FROM student WHERE upper(last) BETWEEN "SMATH" AND "SMZTH"
    ```
    (A부터 Z까지)


<br><br>

## Reference
* http://egloos.zum.com/heyjoon/v/2762501

추가
* https://bencrow.tistory.com/entry/25%EA%B0%80%EC%A7%80-%ED%9A%A8%EC%9C%A8%EC%A0%81%EC%9D%B8-SQL-%EC%9E%91%EC%84%B1%EB%B2%95
