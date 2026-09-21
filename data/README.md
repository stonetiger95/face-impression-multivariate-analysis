# Data access

이 저장소에는 얼굴 사진과 raw ratings를 포함하지 않습니다.

## Dataset

- Dataset: Face Evaluation Data Set (Karolinska), 14 trait judgments
- Distribution page: https://tlab.uchicago.edu/db-redirect-karolinska-faces/
- Original paper: Oosterhof, N. N., & Todorov, A. (2008). *The functional basis of face evaluation*. https://doi.org/10.1073/pnas.0805664105
- Face stimulus source: Karolinska Directed Emotional Faces (KDEF), Lundqvist, Flykt, & Öhman (1998)

공식 배포 페이지의 안내에 따라 파일을 받은 뒤, 참가자별 표준화 평정의 얼굴별 평균이 들어 있는 파일을 아래 이름으로 저장합니다.

```text
data/Karolinska_14trait_judgmentswithlabels.xls
```

분석 코드는 66개 얼굴 자극, 14개 평정 변수, `Karolinska Label`, `Todorov Label`, `gender` 열을 확인한 뒤 실행됩니다.

## Why raw data is not included

KDEF 공식 조건은 얼굴 자극의 무단 재배포를 금지합니다. 평정 데이터는 연구실 페이지에서 내려받을 수 있지만 별도 재배포 라이선스가 명확히 표시되지 않았습니다. 따라서 공개 GitHub 저장소에는 사진과 평정 파일을 모두 포함하지 않고, 공식 획득 경로만 제공합니다.

- KDEF terms: https://kdef.se/faq/using-and-publishing-kdef-and-akdef
- KDEF copyright holder: Karolinska Institutet, Psychology section

`psychology_data.csv`는 원 과제 폴더에 있었지만 threatening 변수가 빠진 13-trait 변형본이며, 공식 14-trait 파일과 값의 표준화 방식도 다릅니다. 공개 분석 입력으로 사용하지 않았습니다.
