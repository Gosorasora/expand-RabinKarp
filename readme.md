# expand-RabinKarp  
[알고리즘] 유전체 시드 정렬기 — Rabin-Karp 확장 (Bloom Filter + LSH + BandDP)

본 프로젝트는 Rabin-Karp 문자열 탐색 알고리즘을 기반으로, Bloom Filter, *ocality Sensitive Hashing (LSH), Banded Dynamic Programming (BandDP)를 결합하여 오차 허용 기반의 short-read alignment를 수행하는 정렬 알고리즘 구현한 것입니다.

---

## 📂 프로젝트 파일 설명

| 파일명 | 설명 |
|--------|------|
| `expand_RabinKarp.cpp` | 최종 알고리즘 구현 코드 (C++) |
| `smallinput.txt` | reference 서열 데이터 |
| `smallread.txt` | reference에서 추출된 reads 데이터 |
| `result.txt` | 알고리즘 실행 결과 파일 |

---

## ⚙️ 실행 방법

```bash
g++ expand_RabinKarp.cpp -o aligner
./aligner
```

---

## 🧩 알고리즘 구성

- **Bloom Filter** : 존재하지 않는 시드를 빠르게 필터링  
- **LSH (Locality Sensitive Hashing)** : 유사 시드를 같은 버킷에 묶어 후보 축소  
- **BandDP (Banded Edit Distance)** : 허용 오차 D 내에서 정밀 매칭 수행  
  - Band 폭 설정: `2D + 1 → (2D + 1) / 2`  
  - 복잡도: `O(D·L)`  
  - 슬라이딩 윈도우 방식으로 적용  

---

## 🧠 주요 특징

- **정확도 향상**: 단순 mismatch가 아닌 삽입/삭제까지 고려  
- **Early Stopping**: 허용 오차 D 초과 시 조기 중단  
- **Filter 기반 구조**: Bloom + LSH로 후보군을 최소화 후 BandDP 수행  
- **Trade-off 제어 가능**: D 값을 통해 속도·정확도 균형 조정  

---

## 📸 결과 폴더

- `result.txt` : 매칭된 read 인덱스 및 위치, 오차값 출력  
- `experiment/` : 실행 결과 캡처 이미지 (성능 및 정확도 비교)  

---

## 🧾 참고
> 본 프로젝트는 “Rabin-Karp 기반 근사 문자열 매칭 효율화”를 목적으로 한  
> 알고리즘 실험 프로젝트로, 실제 short-read aligner의 경량화 버전 구현입니다.
