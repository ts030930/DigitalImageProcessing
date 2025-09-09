# 빛과 EM 스펙트럼

사람이 볼 수 있는 영역은 EM 스펙트럼의 극히 일부이다.


<img width="35" height="39" alt="image" src="https://github.com/user-attachments/assets/c7776efe-3be4-430a-a4b6-163223bfd3d6" />

<img width="57" height="34" alt="image" src="https://github.com/user-attachments/assets/a9a11cac-72c2-4446-8f06-1b3a6b853d27" />

주파수(v)는 파장과 반비례 관계이고 에너지와는 정비례 관계이다.

<img width="587" height="335" alt="image" src="https://github.com/user-attachments/assets/e46d3347-d8d7-42e1-b628-86541603c262" />

**레이디언스(radiance)** : 광원으로부터 흘러나오는 총 에너지양이며 와트(W) 단위로 측정된다.
 
**루미넌스(luminance)** : 광원으로부터 관찰자가 인지하는 에너지양에 대한 척도를 제공하며 루메(lm)단위로 측정된다.

**명도(brightness)** : 실제로는 측정이 불가능한 빛 인지에 관한 주관적인 측도이다.

# 영상 형성 모델

영상을 f(x,y) 형태의 2D 함수로 표기하고, 공간좌표 (x,y)에서의 f값 또는 진폭은 물리적 의미가 영상의 광원에 의해 결정되는 스칼라양이다.
그러므로 f(x,y)는 음수가 아니고 유한해야한다.

<img width="153" height="37" alt="image" src="https://github.com/user-attachments/assets/faa013c2-c6db-4f40-a8a7-65a17ff6afaf" />

<img width="207" height="194" alt="image" src="https://github.com/user-attachments/assets/99aafa14-aa04-4f3c-88d1-1b858b4d668a" />


이때 f(x,y)는 두 성분, 1) 관찰되는 장면에 입사하는 광원 조명의 양, 2) 장면의 객체에 의해 반사되는 조명의 양에 의해 특정지어 진다.
이떄 각각을 **조명(illumination) 성분**과 **반사(reflection) 성분**이라고 하며 두 값을 곱해서 모델을 형성한다.

# 샘플링(Sampling)과 양자화(Quantization)

**샘플링(Sampling)** : 좌표값을 x,y로 디지털화 하는 것
**양자화(Quantization)** : 진폭값을 디지털화하는 것

# 디지털 영상 표현

<img width="542" height="161" alt="image" src="https://github.com/user-attachments/assets/a14a4073-af6b-4c2a-8fe2-ac9397803c57" />

**이산적인 강도 수준 (Discrete Intensity Levels)**

<img width="756" height="125" alt="image" src="https://github.com/user-attachments/assets/4a44aeb8-62c4-4551-accd-4eec37eabe44" />

K = 1 : (0,1) 흑백
K = 8 : (0,255) 그레이 스케일
k = 3 * 8 = 24 : RGB 스케일

이떄 차지하는 Storage의 크기는 
<img width="187" height="86" alt="image" src="https://github.com/user-attachments/assets/04b80eab-08ef-48b4-8bac-7b25cfa0319c" />
과 같다.

M.N 배열의 채널이 k 만큼 있다고 생각해보면 이해가 쉽다.

# 영상 보간법 (Image Interpolation)

보간법은 알려지지 않은 장소에서의 값을 추정하기 위해 알려져 있는 데이터를 사용하는 방식이다.

**Nearest Neighbor 보간법** : 근접의 pixel들을 사용한다.

**Bilinear Interpolation 보간법** : 4개의 최근접 이웃들을 사용한다.

**Bicubic Interpolation 보간법** : 16개의 이웃들을 사용한다. (가장 부드럽고 높은 퀄리티)


# 픽셀간의 기본 관계

## 픽셀 이웃

<img width="924" height="397" alt="image" src="https://github.com/user-attachments/assets/483c92b3-da87-4756-94ad-f90c36960f90" />

## 인접성(adjacency)

인접성을 정의하는데 사용된 밝기값의 집합을 V로 놓자. 이진 영상에서 만일 우리가 1을 갖는 픽셀들의 인접성을 말하고 있다면 V ={1}이다.

1. 4-인접성 : V로부터의 값을 갖는 두 픽셀 pdhkq는 만일 q가 집합 N4(p)에 있으면 인접한다.
2. 8-인접성 : V로부터의 값을 갖는 두 픽셀 pdhkq는 만일 q가 집합 N8(p)에 있으면 인접한다.
3. m-인접성 : 4-인접성과 8-인접성을 섞었을때, A) q가 p의 4-인접성이 있을때 B) q가 p의 대각선 이웃이면서 p와 q 사이의 두개의 4-인접성이 V에 없을때

m-인접성을 사용하는 이유는 8-인접성에서 나타나는 모호성을 해셜하기 위해서 사용한다.

## 연결성 

두 픽셀 p = (x₀, y₀), q = (xₙ, yₙ)이 S에서 연결되었다(connected in S) 는 의미: p에서 q로 가는 경로(path) 가 존재하며, 그 경로가 S 안의 픽셀들만 사용해서 만들어질 수 있을 때.

이때 연결성분(Connected Component)의 정의는 어떤 픽셀 p ∈ S에서 출발해 연결될 수 있는 픽셀들의 집합이다.


## 영역

### Adjacent와 Disjoint

영역(R)은 두가지 관계를 가질 수 있는데,

1. **Adjacent (인접)**: Ri​∪Rj​(두 영역의 합집합)이 연결되어 있으면 두 영역은 인접하다고 한다.
2. **Disjoint (분리됨)** : 두 영역이 인접하지 않으면, 즉 완전히 떨어져 있으면 disjoint.

이때 **연결**을 정할때 4,8,m-인접성을 고려하는것이다.

<img width="80" height="118" alt="image" src="https://github.com/user-attachments/assets/66d0322f-99db-4465-a795-b9846e1d78d5" />

### Foreground와 Background

**Boundary** : 어떤 영역 R의 boundary(경계) = R에 속하지만, 이웃 중 하나 이상이 R 바깥에 있는 픽셀들을 의미한다.

**전경(Foreground)** :우리가 관심 있는 물체(object of interest)로, 보통 R₁, R₂, …, Rₖ 와 같이 여러 개의 disjoint region(서로 떨어져 있는 영역)으로 구성되어 이 영역들의 합집합이 전체 전경이 된다.
**배경(Background)** : 전경을 제외한 나머지로, 즉 전경의 여집합이다.


## 거리 척도(Distance Measures)

 Distance Function D : 두 픽셀이 얼마나 떨어져있는지를 수치로 나타낸 것.

 **거리 함수의 조건** : 1) **Non-negative (비음수성)** : D(p,q)≥0, D(p,q)=0 ⟺ p=q
                        2) **Symmetry (대칭성)** : D(p,q)=D(q,p)
                        3) **Triangle Inequality** (삼각 부등식) : D(p,z)≤D(p,q)+D(q,z)

### 3가지 방식 

<img width="913" height="407" alt="image" src="https://github.com/user-attachments/assets/7a5bbbf1-dfe3-4c07-a39e-6a514b61de37" />
<img width="802" height="273" alt="image" src="https://github.com/user-attachments/assets/a5fc23ce-2f2b-4cef-a3d7-04a556da2825" />


#  Digital Image Processing – Lecture 2a  
기본 영상 연산 (Basic Operations in Image Processing)

---

# 산술 연산 (Arithmetic Operations)

- 이미지 간의 산술 연산은 배열 연산과 동일하다:

<img width="972" height="486" alt="image" src="https://github.com/user-attachments/assets/9941717e-2a9e-4cc9-ac0d-085f5c393cf2" />

- 선형성 : 
<img width="912" height="390" alt="image" src="https://github.com/user-attachments/assets/064f5a45-6471-4649-9d2b-4d4d051ab158" />

ex) max 연산
<img width="959" height="403" alt="image" src="https://github.com/user-attachments/assets/61499992-f830-4ad9-b609-4e5754a28923" />

---

### 영상 덧셈 (Image Addition)

- 두 장을 합쳐 **Double Exposure** 또는 **Composite** 생성
- 노이즈 제거에 활용 가능

**노이즈 평균화**:

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;\bar{g}(x,y)=\frac{1}{K}\sum_{i=1}^K&space;g_i(x,y))

- 랜덤 노이즈는 평균을 내면 줄어듦  
- 분산은 

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;\frac{1}{K})

배 감소

---

###  영상 뺄셈 (Image Subtraction)

g(x,y)=f(x,y)-h(x,y)
- `f(x,y)` : **Live image** (조영제를 주입한 후 촬영한 영상)  
- `h(x,y)` : **Mask image** (조영제를 주입하기 전 촬영한 영상)  
- `g(x,y)` : **Subtracted image** (두 영상의 차이만 남긴 결과)
- 차분 영상으로 **변화 탐지** 가능  

1. **Mask Image (h(x,y))**  
   - 조영제를 주입하기 전 X-ray 영상 촬영  
   - 뼈와 배경이 포함된 기본 영상  

2. **Live Image (f(x,y))**  
   - 조영제를 주입한 후 다시 촬영한 X-ray 영상  
   - 혈관 속 조영제가 보이기 시작  

3. **Subtraction (g(x,y))**  
   - `f(x,y) - h(x,y)` 연산 수행  
   - 배경(뼈, 고정된 조직)은 상쇄되어 제거  
   - 혈관(조영제가 흘러간 부분)만 남음  
---

#  집합 & 논리 연산 (Set and Logical Operations)

## 회색조 영상의 집합 표현

gray scale image는 
<img width="855" height="175" alt="image" src="https://github.com/user-attachments/assets/336b4828-faee-45f9-8f6c-f445e43cd644" />

다음과 같이 표현가능하다

## 보수 (Complement)

<img width="844" height="147" alt="image" src="https://github.com/user-attachments/assets/72d3b6a7-6717-45ed-8d9a-370e978d462a" />

- 예: 8비트 영상 (\(k=8\)) → \(K=255\)  
- 픽셀 값 200 → 보수 = 55  

---

# 공간 연산 (Spatial Operations)

## 1. 단일 픽셀 연산 (Single-pixel Operation)
픽셀 값 변환 함수:

<img width="1167" height="585" alt="image" src="https://github.com/user-attachments/assets/b689e5de-e8c2-400c-82d6-9db15f66d09a" />


---

## 2. 이웃 기반 연산 (Neighborhood Operations)
- 주변 픽셀 고려 (3×3, 5×5 등)  
- **예시**:
  - 스무딩 (평균, 노이즈 제거)  
  - 샤프닝 (에지 강조)  
  - 미디언 필터  
  - 엣지 검출  

---

## 3. 기하학적 공간 변환 (Geometric Spatial Transformations)

- 이동, 회전, 확대/축소, 기울이기(왜곡) 포함
- 기본 변환식 :
<img width="729" height="137" alt="image" src="https://github.com/user-attachments/assets/ea49cc97-863e-4fff-9a75-122bb1d7d850" />

- 아핀 변환식:

<img width="743" height="690" alt="image" src="https://github.com/user-attachments/assets/2e4138a6-7d23-45a6-9331-435fc52b8707" />

---

## 영상 정합 (Image Registration)

두 장 이상의 동일 장면 이미지를 서로 맞추는 과정. 
- **Tie points (제어점)** 활용  

**Bilinear Approximation Model**:

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;x=c_1v+c_2w+c_3vw+c_4)

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;y=c_5v+c_6w+c_7vw+c_8)

- 4쌍의 대응점 → 8개의 방정식 → 파라미터 계산  

---

##  영상 변환 (Image Transform)

영상 → 다른 표현 공간으로 변환  
- 목적: 압축, 잡음 제거, 특징 추출 등

### 2D 이산 푸리에 변환 (2D DFT)

- 공간 영역 영상 ![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;f(x,y)) → 주파수 영역 ![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;T(u,v))  
- 역변환으로 원본 복원 가능  

---

## 확률적 방법 (Probabilistic Methods)

### 픽셀 강도의 확률

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;p(z_k)=\frac{n_k}{MN},\quad\sum_{k=0}^{L-1}p(z_k)=1)

- \(n_k\): 강도 \(z_k\)를 가진 픽셀 개수  
- \(MN\): 전체 픽셀 수  

---

### 평균 (Mean Intensity)

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;m=\sum_{k=0}^{L-1}z_kp(z_k))

- 평균 낮음 → 어두운 영상  
- 평균 높음 → 밝은 영상  

---

### 분산 (Variance)

![equation](https://latex.codecogs.com/png.image?\dpi{150}&space;\sigma^2=\sum(z_k-m)^2p(z_k))

- **분산 작음** → 저대비 (flat)  
- **분산 큼** → 고대비 (sharp)  

---

# 정리

- 산술 연산: 덧셈(노이즈 제거), 뺄셈(변화 탐지)  
- 집합 연산: 보수, 논리 연산  
- 공간 연산: 단일 픽셀, 이웃 연산, 기하학적 변환  
- 영상 정합: Bilinear 모델  
- 변환: 2D DFT 등  
- 확률적 방법: 픽셀 분포, 평균, 분산  

---


