# Analysis notes

## Scope

공개용 분석은 원 과제의 기술통계, 상관분석, Mardia 다변량 정규성 검정, PCA, PCFA, MLFA with Varimax rotation, hierarchical clustering, NbClust, K-means, 군집과 자극 성별의 관계를 재검토했다. 새로운 모델이나 복잡한 군집 안정성 검증은 추가하지 않았다.

## Source review

검토한 원본은 `analysis.Rmd`, `analysis_output.html`, `report.docx`, `dataset_readme.txt`, `psychology_data.csv`, `trait_labels.xls`이다. 원본 폴더는 수정하지 않았다.

원 과제는 별도 원본 프로젝트에 보존되어 있다. 공개 저장소에서는 작성자 개인정보, seed 미고정 당시의 오래된 결과, 재배포 조건이 명확하지 않은 부속 파일 때문에 원본 사본을 제외했다.

- `trait_labels.xls`: 66 × 17 구조. 식별자 2개, gender 1개, 14개 평정 변수를 포함한다.
- `psychology_data.csv`: 66 × 14 구조. Face와 13개 평정만 있으며 `threatening`이 없다. 값도 XLS와 다른 표준화 버전이다.
- 원 Rmd는 실제 폴더에 없는 `Karolinska_14trait_judgmentswithlabels.xls`를 참조했다.
- 최종 Word 보고서는 군집-성별 결과를 제거하고, seed 미설정으로 결과가 달라졌다고 기록했다.

## Reproduced results

- PCA (covariance-based, unscaled): PC1 64.467%, PC2 18.074%, cumulative 82.541%.
- PCFA (correlation matrix): first two components 62.846% and 18.930%, cumulative 81.776%.
- MLFA with Varimax: SS loadings 6.819 and 4.302, cumulative proportion 79.436%.
- Mardia skewness: p = 0.6761. Mardia kurtosis: p = 0.1858.
- NbClust majority: 9 indices proposed 3 clusters, 7 proposed 2, 2 proposed 4, 2 proposed 5, 1 proposed 7, and 2 proposed 10.

## Statistical issues and handling

### K-means reproducibility

원 코드의 `kmeans(Z, 3)`에는 seed가 없었다. 공개용 분석은 결과 비교 전에 재현성을 위해 `set.seed(2025)`를 고정했으며 seed 탐색을 하지 않았다. 결과적으로 최종 Word 보고서의 군집 크기 25/17/24와 모든 군집 중심이 재현됐다.

군집 중심을 기준으로 보면 기존 본문의 군집 명칭 일부는 표와 일치하지 않았다. 고정 seed 결과에서는 Cluster 1이 긍정적·친사회적, Cluster 2가 부정적·위협적, Cluster 3이 평균에 가까운 저지배 패턴이다. 공개용 문서는 중심값에 맞춰 표현을 수정했다.

### Cluster stability

기존 분석에는 silhouette 또는 bootstrap stability 검증이 없다. 새 분석을 추가하지 않고 결과를 `exploratory clusters`로 제한했다. 군집 번호는 본질적 유형명이 아니다.

### Number of factors

두 요인 선택은 scree plot, 설명력, 기존 연구의 2차원 구조를 근거로 했다. parallel analysis, KMO, Bartlett 검정은 기존에 없었으므로 새로 추가하지 않았다. 이를 요인 수 선택의 한계로 기록했다.

### Multivariate normality

Mardia 검정 p-value가 0.05보다 컸다는 결과는 재현됐다. 공개용 문구는 “다변량 정규성을 만족한다”가 아니라 “정규성을 기각할 충분한 근거가 없었다”로 수정했다.

### MLFA fit

원 보고서는 높은 설명량과 잔차 상관을 근거로 2-factor MLFA의 적합성이 높다고 서술했다. 그러나 `factanal()`의 exact-fit test는 χ²(64) = 257.88, p < .001이었다. 공개용 문서는 2-factor 구조의 해석적 유용성과 exact-fit 부족을 함께 기록했다.

### PCA and PCFA explained variance

원 문서에는 PCA와 PCFA가 모두 약 82.6%라고 적힌 부분이 있다. 실제 재계산값은 covariance-based PCA 82.5%, correlation-based PCFA 81.8%이다. 방법에 따라 입력 행렬이 달라 생기는 차이이며 공개용 수치를 구분했다.

공분산 기반 PCA는 원 분석을 보존하기 위한 선택이다. 평균 평정 변수의 표준편차가 서로 다르므로 표준편차가 큰 변수가 PCA에 더 큰 영향을 줄 수 있다는 점을 한계로 명시했다.

### Analysis unit

관측치는 참가자가 아니라 참가자 평정을 평균한 얼굴 자극 66개다. 모든 해석은 평균화된 자극 수준에 한정했다.

### Gender association

원 Rmd에는 seed가 고정되지 않은 군집으로 p = 0.0275가 보고됐지만, 고정 seed 결과는 χ²(2) = 1.696, p = 0.428이었다. 최종 Word 보고서는 이 절을 제거했다. 공개용 분석은 고정 seed 결과만 보조적으로 제시하며, 사회적 고정관념이나 남녀 일반의 심리 차이로 확대하지 않는다.

## Reproducibility boundary

raw data는 재배포 라이선스가 불명확해 저장소에서 제외했다. 공식 파일을 지정 경로에 둔 로컬 검증에서는 R 4.6.1로 전체 Rmd와 HTML, 4개 Figure를 생성했다. 데이터가 없는 신규 clone에서는 `data/README.md`의 획득 절차가 선행되어야 한다.
