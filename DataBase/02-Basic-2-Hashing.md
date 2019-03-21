# Database Basics #2
Hashing
> 19-03-21 (목)

<br>

### 순서
1. Static Hashing
2. Dynamic Hashing
3. Ordered Indexing & Hashing 비교
4. Multiple Key Access
5. Bitmap Index


<br><br>


# 1. Static Hashing
- bucket: 1개 이상의 record를 저장하는 단위
- search-key와 hash function으로 bucket 위치를 얻어낸다.
- search-key 값이 달라도 같은 위치에 저장될 수 있다. (충돌)

### 단점
- 데이터베이스가 커지면서 성능 문제 발생 가능 (overflow)
- 이를 개선하기 위해 실제로 사용될 양보다 많은 space를 잡아 놓으면 공간 낭비
- 해결 방법 중 하나는 재배치. 하지만 연산에 비용이 크다.



<br><br><br>

# 2. Dynamic Hashing
Static Hashing의 단점을 보완하기 위해 다이나믹 해싱이 등장했다.

- 크기가 늘어나고 줄어드는 데이터베이스에 적합하다.
- hash function이 dynamic하게 수정되는 것을 허용
- Extendable Hashing (dynamic hashing의 한 종류)


<br><br><br>

# 3. Ordered Indexing vs Hashing
#### Point Query
- (point query) 특정 값을 가진 key를 찾을 때는 hash
- 더 빠름

#### Range Query
- range 쿼리는 hash가 별로 의미 있지 않다.
- 이런 경우에는 돌면서 확인하면 됨 (정렬된 index니까)
- (각 연산 자체는 hash보다 느림)


<br><br><br>

# 4. Multiple-Key Access

아래와 같이 `and`가 있는 경우 각 조건에 대해서 연산 가능하다.
```sql
SELECT	ID
FROM	instructor
WHERE	dept_name = “Finance” and  salary = 80000
```
#### 가능한 방법
1) index로 `dept_name`이 "Finance"인 것을 찾고 그 row들에 대해서 `salary`가 80000인지 검사
2) `salary`가 80000인 것을 먼저 모두 찾고 `dept_name`이 "Finance"인지 확인
3) 각각 가져와서 교집합

그게 아니라면?

`(dept_name, salary)`라는 형태의 combined search-key를 만든다.

- 이 때 질의의 순서도 중요하다.
- WHERE절에서 dept_name에 대한 point query AND salary에 대한 range query 순으로 조건을 주었을 때 더 빠르다.
- (dept_name에 대한 range AND salary에 대한 point보다)


<br><br><br>


# 4. Bitmap Indices

- 비교적 적은 개수의 서로 다른(distinct) 값
- 일반적으로 array of bits로 표현된다.
- 다중 키에 대한 연산이 쉬워짐. (bit 연산으로 조건을 판단하면 되기 때문)

