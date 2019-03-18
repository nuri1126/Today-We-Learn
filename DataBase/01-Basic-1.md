# Database Basics #1
Indexing & Hashing

> 19-03-18 (월)
> <a href="https://github.com/jinnyy">@jinnyy</a>

<br>

### 순서
0. 기본 개념
1. Ordered Index
2. B+-Tree & B-Tree


[참고] B-tree와 B+-tree는 <a href="https://github.com/nuri1126/Today-We-Learn/tree/master/DataStructure">DataStructure</a>에서 더 자세히 다룹니다.



<br><br><br>
# 0. 기본 개념
* Indexing은 원하는 data에 더 빠르게 접근하기 위해 사용됨
* Search key: 파일의 record를 찾는 데 사용되는 attribute들의 set(집합)
* index file
    - index entry라고 불리는 레코드들로 이루어짐
    - 보통 원래 파일보다는 훨씬 작음
* Index의 두 가지 타입
    - Ordered index: Search key가 정렬돼서 저장
    - Hash index: Search key가 hash 함수에 따라 bucket들에 일정(균일)하게 분포


<br><br>

# 1. Ordered Index
* 인덱스 entry가 search key 값으로 정렬돼서 저장됨
* 종류
    - Primary Index (clustering index): 파일의 sequential 순서와 같음
    - Secondary Index (non-clustering index): 파일의 sequential 순서와 다름
* Indexed Sequential File: primary index로 정렬된 sequential 파일


<br>

### Primary Index
* Multilevel Index: index의 index를 만들어서 구성
* Secondary Index: 정렬 순서가 primary key와 다름
    - 기본적으로 dense해야 함
    - 서치 키 순서대로 접근하지 않음 → 전체를 접근

<br>

#### Dense Index vs Sparse Index

<table style="width:100%">
  <tr>
    <th></th>
    <th>Dense Index</th> 
    <th>Sparse Index</th>
  </tr>
  <tr>
    <td>장점</td>
    <td>레코드 접근이 빠름</td> 
    <td>공간 부하가 적음, 변경이 적음</td>
  </tr>
  <tr>
    <td>단점</td>
    <td>row 추가시마다 index 파일이 바뀜, 공간 부하가 큼</td> 
    <td>조회 속도 느릴 수도</td>
  </tr>
</table>


<br><br>

# 3. B+-Tree & B-Tree

<table style="width:100%">
  <tr>
    <th></th>
    <th>B-Tree</th> 
    <th>B+-Tree</th>
  </tr>
  <tr>
    <td>장점</td>
    <td>데이터 중복이 없음, 노드 수가 적음, leaf까지 도달하기 전에 검색 완료 가능</td> 
    <td>tree 구조가 자동으로 rebalancing됨</td>
  </tr>
  <tr>
    <td>단점</td>
    <td>삘리 검색 가능한 부분은 적은 일부분, Non-leaf 노드가 많아지면 fan-out이 적어짐, 삽입/삭제 더 어려움 (구현 어려움)</td> 
    <td>상위 구조에 의한 삽입/삭제 overhaed가 생길 수 있음</td>
  </tr>
</table>


<br>
