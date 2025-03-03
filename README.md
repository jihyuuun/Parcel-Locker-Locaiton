# YEONGTONG-PARCEL-LOCKER
경기도 영통구 무인택배함 입지 최적화

📅 **기간**: Sep 2024 – Dec 2024 

## 📖 프로젝트 개요  

본 프로젝트는 **MCLP(Maximal Covering Location Problem)** 및 **P-Median** 모델을 활용하여 **경기도 수원시 영통구 내 최적의 무인택배함 입지**를 선정하는 연구입니다. 공공시설을 후보지로 선정하고, **인구와 보행 접근성**을 고려하여 최적의 입지를 분석하는 것이 목표입니다.

## 🔍 프로젝트 필요성
- **1인가구 증가 & 언택트 소비 확산**: 택배 수령이 어려운 1인가구 및 맞벌이 가구 증가
- **택배 도난 및 분실 예방**: 여성 및 부재 가구 대상의 보안 강화
- **친환경 물류 기여**: 배송 경로 최적화로 탄소 배출 감소

## 🛠 사용 기술 및 라이브러리
- **프레임워크**: Python (Jupyter Notebook)
- **수리 최적화**: PuLP, OR-Tools
- **데이터 분석**: Pandas, Geopandas
- **시각화**: Folium, Matplotlib, Seaborn
- **GIS 데이터 처리**: Shapely, Geopandas

## 📂 프로젝트 구조  

```
├── data/                         # 데이터 저장 폴더
│   ├── after/                    # 전처리된 데이터
│   │   ├── p_median_d_variable.csv       # 거리 변수 데이터
│   │   ├── real_p_median_h_variable.csv  # 수요 변수 데이터
│   │   ├── 영통구 공공시설_레알최종본.csv  # 최종 후보지 데이터
├── modeling/                      
│   ├── MCLP.ipynb                 # MCLP 모델 구현 코드
│   ├── pmedian.ipynb              # P-Median 모델 구현 코드
├── preprocessing/               
│   ├── 데이터_전처리_oveall.ipynb  # 데이터 전처리 코드
├── README.md                      # 프로젝트 설명
```

## 📊 데이터 출처 (공공 데이터 포털)

- **경기도 수원시 일 평균 유동인구**
- **국토교통부 국토지리정보원 격자 100m**
- **국토교통부 국토지리정보원 총 인구수**

## 🎯 프로젝트 과정  

### **1️⃣ 데이터 전처리**

- **정규성 검증**: Kolmogorov-Smirnov test
- **등분산성 검증**: Levene’s Test
- **정규화&스케일링**: Yeo-Johnson Transform, Robust Scaler, MinMax Scaler

### **2️⃣ 가중치 설정**  

**K-Means 클러스터링**
- 주거인구 가중치 = 클러스터별 중심점의 주거인구/주거인구+유동인구
- 유동인구 가중치 = 클러스터별 중심점의 유동인구/주거인구+유동인구

### **3️⃣ MCLP**  

$$
\begin{aligned}
    \text{max} \quad & \sum_{i \in I} h_i y_i \\
    \text{s.t.} \quad & \sum_{j \in N_i} x_j \geq y_i, \quad \forall i \in I, \\
    & \sum_{j \in J} x_j = p, \\
    & y_i \in \{0,1\}, \quad \forall i \in I, \\
    & x_j \in \{0,1\}, \quad \forall j \in J.
\end{aligned}
$$

**p개수 선정**

엘보우 포인트를 찾을 수 없음

![image](https://github.com/user-attachments/assets/a4b70acd-4e67-4398-8384-cbfcf73f38a4)


### **4️⃣ P-median**  

$$
\begin{aligned}
    \text{min} \quad & \sum_{i \in I} \sum_{j \in J} h_i d_{ij} y_{ij} \\
    \text{s.t.} \quad & \sum_{j \in J} y_{ij} = 1, \quad \forall i \in I, \\
    & \sum_{j \in J} x_j = p, \\
    & y_{ij} \leq x_j, \quad \forall i \in I, j \in J, \\
    & y_{ij}, x_j \in \{0,1\}, \quad \forall i \in I, j \in J.
\end{aligned}
$$

**p개수 선정**

p=4
![image](https://github.com/user-attachments/assets/a0f25c87-0ef6-493f-b8c1-d8a0c97ba57f)

## 📈 프로젝트 결과

광교 1동 행정복지센터, 매탄 2동 행정복지센터, 수원시립영통도서관, 망포역 공영주차장
![image](https://github.com/user-attachments/assets/44286de1-37f4-43eb-a4e8-1fee768ad5f5)

## 📜 참고 자료

- 문소현 외 (2020). 지역 제한 P-median 모델을 이용한 서울시 주거복지센터 입지 분석 및 모델링. 대한지리학회지, 55(2), 197-206.
- 김태일 외 (2023). 서울시 여성안심택배함 증설 최적 입지 분석. 경영과학, 40(1), 47-59. DOI: 10.7737/KMSR.2023.40.1.047.
- 이해빈 외 (2023). 공공데이터 기반 공영주차장 최적입지 선정을 위한 최대 커버지역 문제(MCLP)해결 기법. 멀티미디어학회논문지, 26(2), 275-287. DOI: 10.9717/kmms.2023.26.2.275.

