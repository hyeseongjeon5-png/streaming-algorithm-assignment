
# 스트리밍 알고리즘 2종 구현 및 정확도·메모리 트레이드오프 분석

## 1. 과제 개요

본 프로젝트는 대용량 데이터 스트림 환경에서 전체 데이터를 저장하지 않고 근사 계산을 수행하는 스트리밍 알고리즘을 구현하고, 정확도·메모리·처리시간 측면에서 성능을 비교하는 것을 목적으로 한다.

## 2. 사용 데이터셋

- 데이터셋: MovieLens 1M
- 사용 파일: ratings.dat
- 레코드 수: 1,000,209개
- 데이터 형식: UserID::MovieID::Rating::Timestamp

본 실험에서는 ratings.dat 파일을 한 줄씩 읽어 처리함으로써 스트리밍 환경을 모사하였다.

## 3. 구현 알고리즘

### 3.1 Bloom Filter

Bloom Filter는 원소의 포함 여부를 근사적으로 판정하는 알고리즘이다.

본 실험에서는 사용자 ID와 영화 ID를 결합한 user_id_movie_id 값을 원소로 사용하였다.

측정 항목은 다음과 같다.

- False Positive Rate
- False Negative Count
- 메모리 사용량
- 처리 시간

### 3.2 Count-Min Sketch

Count-Min Sketch는 스트리밍 데이터에서 항목별 빈도를 근사적으로 추정하는 알고리즘이다.

본 실험에서는 영화 ID별 등장 빈도를 추정하였다.

측정 항목은 다음과 같다.

- 평균 절대 오차
- 평균 상대 오차
- 최대 오차
- 메모리 사용량
- 처리 시간

## 4. 실험 결과 요약

### Bloom Filter

비트 배열 크기와 해시 함수 개수가 증가할수록 False Positive Rate는 감소하였다.

하지만 메모리 사용량과 처리 시간은 증가하였다.

### Count-Min Sketch

width와 depth가 증가할수록 평균 상대오차는 감소하였다.

하지만 메모리 사용량과 처리 시간은 증가하였다.

## 5. 결론

두 알고리즘 모두 정확도를 높이기 위해서는 더 많은 메모리와 처리 시간이 필요하다는 trade-off가 확인되었다.

Bloom Filter는 포함 여부 판정에 적합하고, Count-Min Sketch는 항목별 빈도 추정에 적합하다.

실제 서비스 로그 분석에서는 클릭 수, 조회 수, 이벤트 발생 빈도와 같은 빈도 추정이 중요하므로 Count-Min Sketch가 더 실용적이라고 판단하였다.

## 6. 실행 방법

1. 저장소를 다운로드한다.
2. Jupyter Notebook에서 streaming_algorithm_assignment.ipynb 파일을 실행한다.
3. 노트북 실행 시 MovieLens 1M 데이터셋이 자동으로 다운로드된다.
4. 실험 결과는 results 폴더에 CSV로 저장되고, 그래프는 figures 폴더에 저장된다.

## 7. 폴더 구조

streaming_algorithm_assignment/
- streaming_algorithm_assignment.ipynb
- README.md
- .gitignore
- figures/
- results/
