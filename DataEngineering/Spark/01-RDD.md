# RDD
Resilient Distributed Datasets
> 19-03-31 <a href="https://github.com/jinnyy">@jinnyy</a>


<br>

- HDFS를 거치려면 디스크를 거쳐야 해서 느린 것 같다. -> RAM을 사용해서 속도를 높여보자

- RAM에 올림으로써 속도를 높인다.
- (HDFS처럼) Read-Only로 + lineage 기록 -> fault tolerant


<br><br><br>


## 1. 특징 요약
* Immutable, partitioned
* storage -> RDD / RDD -> RDD 만 가능

<br><br>

## 2. lazy execution
* `Transformation`: 어떻게 바꿀 지 기록 (lineage 생성)
* `Action`: lineage로 생성한 명령들 실제로 수행

참고: lineage는 DAG(Directed Asyclic Graph)로 구현됨


#### 좋은점
* 상황을 미리 고려해서 자원을 효율적으로 사용할 수 있음 (최적의 방법 계획 가능 `job scheduling`)


<br><br>

## 3. Dependency
#### Narrow Dependency
작업을 한 노드에서 모두 할 수 있음
* 네트워크 비용 X
* 속도 빠름
* 파티션이 망가져도 복원 가능

#### Wide Dependency
서로 다른 곳에 저장돼있어서 불러오려면 shuffle해야 하는 것들
* 네트워크 비용 ++
* 중간에 오류나면 손실
* 이런 경우는 추가적인 checkpointing 좋을 수도

<br><br>

## 4. Job Scheduling
* (lineage) DAG에 따라 계산
* 이미 계산이 끝난 파티션은 다시 계산하지 않음
* 필요한 파티션 추가적으로 생성하며 결과 생성
* 파티션이 수행될 노드는 data locality를 고려해서 생성됨 (특히 HDFS)


<br><br><br>

### Reference
* https://www.slideshare.net/yongho/rdd-paper-review ☆
* https://www.usenix.org/system/files/conference/nsdi12/nsdi12-final138.pdf
