# WebSea Landing 디자인 시스템 문서

> 이 문서는 WebSea Landing 프로젝트의 디자인 시스템을 정리한 것으로, 다른 프로젝트에 재사용할 수 있도록 작성되었습니다.

## 목차

1. [디자인 철학](#디자인-철학)
2. [컬러 시스템](#컬러-시스템)
3. [타이포그래피](#타이포그래피)
4. [간격 시스템](#간격-시스템)
5. [반응형 디자인](#반응형-디자인)
6. [컴포넌트 스타일](#컴포넌트-스타일)
7. [애니메이션](#애니메이션)
8. [레이아웃 시스템](#레이아웃-시스템)
9. [디자인 토큰](#디자인-토큰)
10. [적용 가이드](#적용-가이드)

---

## 디자인 철학

### 전체 컨셉
- **다크 테마 사이버펑크/핀테크 스타일**: 깊은 다크 배경에 네온 그린 악센트
- **글래스모피즘**: 반투명 카드와 블러 효과
- **마이크로 인터랙션**: 호버, 스크롤, 상태 변화에 섬세한 애니메이션
- **한글 우선 디자인**: 한글 타이포그래피 네이티브 지원
- **접근성 친화적**: 텍스트와 배경의 높은 대비, 명확한 시각적 위계

### 핵심 원칙
1. **미니멀리즘**: 여백을 전략적으로 활용한 깔끔한 레이아웃
2. **애니메이션을 통한 강조**: 모션으로 중요 요소에 시선 유도
3. **일관성**: 예측 가능한 반복 패턴
4. **반응형 우선**: 768px 브레이크포인트에서 모바일 고려
5. **성능**: 무겁지 않은 효율적인 CSS

---

## 컬러 시스템

### CSS 변수 정의

```css
:root {
  /* Primary Colors */
  --primary-dark: #1a1d29;      /* 메인 섹션 다크 배경 */
  --primary-darker: #0f1117;    /* 오버레이/내비게이션 최고 어두움 */

  /* Accent Colors */
  --accent-green: #a4ff3d;      /* 주요 브랜드 컬러 - 라임 그린 */
  --accent-green-dark: #8fde35; /* 어두운 그린 변형 */
  --accent-green-light: #c5ff7a;/* 밝은 그린 변형 */

  /* Text Colors */
  --text-light: #ffffff;        /* 주요 텍스트 - 화이트 */
  --text-gray: #a0a3b5;         /* 보조 텍스트 - 음소거된 그레이 */

  /* System Colors */
  --color-danger: #ff6b6b;      /* 리스크/경고 - 레드 */
  --color-loss: #ff4d4d;        /* 손실 값 - 진한 레드 */

  /* Gradients */
  --gradient-1: linear-gradient(135deg, #a4ff3d 0%, #8fde35 100%);
  --gradient-2: linear-gradient(135deg, #c5ff7a 0%, #a4ff3d 50%, #8fde35 100%);

  /* Shadows */
  --shadow-glow: 0 0 40px rgba(164, 255, 61, 0.3);
}
```

### 컬러 사용 가이드

| 용도 | 컬러 | 사용 예시 |
|------|------|-----------|
| **배경** | `#1a1d29`, `#0f1117` | 섹션 배경, 카드 배경 |
| **인터랙티브** | `#a4ff3d` | 버튼, 링크, 호버 상태 |
| **강조** | `#a4ff3d` ~ `#c5ff7a` | 제목 그라데이션, 아이콘 |
| **주요 텍스트** | `#ffffff` | 제목, 본문, 라벨 |
| **보조 텍스트** | `#a0a3b5` | 설명, 비활성 상태 |
| **경고/손실** | `#ff6b6b`, `#ff4d4d` | 리스크 표시, 손실 금액 |

### 투명도 스케일

```css
/* 자주 사용되는 투명도 값 */
0.9   /* 불투명 배경 (내비게이션 바) */
0.8   /* 높은 투명도 텍스트 오버레이 */
0.5   /* 중간 투명도 카드 */
0.3   /* 글로우/섀도우 효과 */
0.2   /* 테두리 색상 */
0.15  /* 섬세한 테두리 */
0.1   • 매우 연한 테두리, 배경 */
0.05  /* 최소 투명도 오버레이 */
```

### 그라데이션 패턴

```css
/* 버튼 그라데이션 */
background: linear-gradient(135deg, #a4ff3d 0%, #8fde35 100%);

/* 제목 텍스트 그라데이션 (shimmer 효과용) */
background: linear-gradient(
  90deg,
  #c5ff7a 0%,
  #a4ff3d 50%,
  #8fde35 100%
);

/* 카드 배경 그라데이션 */
background: linear-gradient(
  135deg,
  rgba(26, 29, 41, 0.5) 0%,
  rgba(15, 17, 23, 0.7) 100%
);

/* 섹션 배경 그라데이션 */
background: linear-gradient(
  180deg,
  transparent 0%,
  rgba(26, 29, 41, 0.3) 100%
);
```

---

## 타이포그래피

### 폰트 패밀리

```css
/* Google Fonts 임포트 */
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Noto+Sans+KR:wght@300;400;500;700&display=swap');

/* 디스플레이/헤딩 폰트 */
font-family: 'Orbitron', sans-serif;
/* 사용처: 메인 제목(h1, h2), 섹션 타이틀, 로고, 숫자/통계, 단계 표시 */
/* 가중치: 400, 700, 900 */

/* 본문/콘텐츠 폰트 */
font-family: 'Noto Sans KR', sans-serif;
/* 사용처: 본문 텍스트, 문단, 라벨, 내비게이션 링크 */
/* 가중치: 300, 400, 500, 700 */
```

### 폰트 크기 스케일

| 컴포넌트 | 데스크톱 | 모바일 | 컨텍스트 |
|----------|----------|--------|----------|
| **Hero h1** | 4.5rem (72px) | 2.5rem (40px) | 메인 헤딩 |
| **섹션 타이틀** | 3rem - 3.5rem | 2rem | 주요 섹션 |
| **리스크 섹션 h2** | 3.5rem | 2rem | 서브섹션 |
| **단계 번호** | 4rem | - | 원형 배지 |
| **리스크 항목 h3** | 3rem | 2rem | 리스크 카드 제목 |
| **Hero h2** | 1.5rem | 1.2rem | 서브타이틀 |
| **기능 카드 h3** | 1.6rem | - | 카드 제목 |
| **단계 콘텐츠 h3** | 1.8rem | - | 단계 라벨 |
| **솔루션 박스 h3** | 2.5rem | 1.8rem | 기능 하이라이트 |
| **본문 텍스트** | 1.1rem - 1.4rem | 1rem - 1.1rem | 일반 콘텐츠 |
| **라벨** | 0.9rem - 1.2rem | 0.9rem | 폼 라벨 |
| **보조 텍스트** | 1rem | - | 도움말 텍스트 |

### 폰트 가중치 사용법

```css
font-weight: 900;  /* 메인 헤딩 (임팩트/강조) */
font-weight: 700;  /* 섹션 타이틀, 버튼, 볼드 텍스트 */
font-weight: 500;  /* 내비게이션, 폼 라벨, 세미볼드 */
font-weight: 400;  /* 본문 텍스트, 일반 가중치 */
font-weight: 300;  /* 서브타이틀, 라이트 가중치 */
```

### 줄 높이

```css
line-height: 1.6 - 2.0;  /* 본문 텍스트 */
line-height: 1.8;        /* 카드 내 문단, 리스트 항목 */
```

### 텍스트 스타일 예시

```css
/* 메인 헤딩 */
.hero h1 {
  font-family: 'Orbitron', sans-serif;
  font-size: 4.5rem;
  font-weight: 900;
  line-height: 1.2;
  background: linear-gradient(90deg, #c5ff7a 0%, #a4ff3d 50%, #8fde35 100%);
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

/* 본문 텍스트 */
p {
  font-family: 'Noto Sans KR', sans-serif;
  font-size: 1.1rem;
  font-weight: 400;
  line-height: 1.8;
  color: #a0a3b5;
}

/* 강조 텍스트 */
.highlight {
  color: #a4ff3d;
  font-weight: 700;
}
```

---

## 간격 시스템

### 패딩 스케일

```css
/* 컴포넌트 레벨 패딩 */
--spacing-xs: 0.5rem;   /* 8px - 인풋 내부 간격 */
--spacing-sm: 1rem;     /* 16px - 버튼 내부 간격 */
--spacing-md: 1.5rem;   /* 24px - 카드 내부 간격 */
--spacing-lg: 2rem;     /* 32px - 섹션 패딩 */
--spacing-xl: 3rem;     /* 48px - 큰 섹션 패딩 */
--spacing-2xl: 4rem;    /* 64px - 대형 컨테이너 패딩 */
--spacing-3xl: 6rem;    /* 96px - 주요 섹션 패딩 */
--spacing-4xl: 8rem;    /* 128px - CTA 섹션 패딩 */

/* 레이아웃 패딩 */
--layout-padding: 5%;   /* 모든 섹션 좌우 패딩 */
```

### 사용 예시

```css
/* 버튼 */
padding: 1.2rem 3rem;

/* 카드 */
padding: 2.5rem;

/* 섹션 */
padding: 6rem 5%;

/* 입력 필드 */
padding: 0.8rem 1rem;
```

### Gap/간격

```css
/* 내비게이션 */
gap: 2rem;              /* 링크 간 간격 */

/* 버튼 그룹 */
gap: 1.5rem;            /* CTA 버튼 간 간격 */

/* 그리드 */
gap: 1.5rem;            /* 설정 그리드 */
gap: 2rem;              /* 기능 카드, 요약 그리드 */
gap: 3rem;              /* 통계 섹션 */

/* 레이아웃 */
gap: 1rem;              /* 카드 내 세로 간격 */
gap: 0.5rem;            /* 라벨-인풋 간격 */
gap: 1.5rem;            /* 섹션 간 마진 */
```

### 마진 스케일

```css
margin: 0;              /* 리셋 */
margin: 0.5rem;         /* 작은 간격 */
margin: 1rem;           /* 단위 간격 */
margin: 1.5rem;         /* 중간 간격 */
margin: 2rem;           /* 표준 섹션 간격 */
margin: 3rem;           /* 큰 섹션 간격 */
margin: 4rem;           /* 주요 섹션 간 간격 */
```

---

## 반응형 디자인

### 브레이크포인트

```css
/* 단일 모바일 브레이크포인트 */
@media (max-width: 768px) {
  /* 태블릿 및 모바일 조정 */
}
```

### 반응형 동작 패턴

| 요소 | 데스크톱 | 모바일 (<768px) |
|------|----------|-----------------|
| **Hero h1** | 4.5rem | 2.5rem |
| **Hero h2** | 1.5rem | 1.2rem |
| **섹션 타이틀** | 3rem | 2rem |
| **CTA 버튼** | flex-direction: row | flex-direction: column |
| **단계** | flex-direction: row | flex-direction: column, text-center |
| **내비게이션 링크** | display: flex | display: none |
| **리스크 아이콘** | 8rem | 5rem |
| **솔루션 박스** | padding: 4rem | padding: 2rem |
| **기능 카드** | flex-direction: row | flex-direction: column |

### 반응형 템플릿

```css
/* 데스크톱 우선 접근 */
.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 6rem 5%;
}

@media (max-width: 768px) {
  .container {
    padding: 3rem 5%;
  }

  h1 {
    font-size: 2.5rem;
  }

  .button-group {
    flex-direction: column;
    gap: 1rem;
  }
}
```

---

## 컴포넌트 스타일

### 버튼

#### Primary 버튼

```css
.btn-primary {
  background: linear-gradient(135deg, #a4ff3d 0%, #8fde35 100%);
  color: #0f1117;
  padding: 1.2rem 3rem;
  font-size: 1.1rem;
  font-weight: 700;
  border: none;
  border-radius: 50px;
  box-shadow: 0 10px 30px rgba(164, 255, 61, 0.3);
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(164, 255, 61, 0.5);
}
```

#### Secondary 버튼

```css
.btn-secondary {
  background: transparent;
  color: #a4ff3d;
  border: 2px solid #a4ff3d;
  padding: 1.2rem 3rem;
  font-size: 1.1rem;
  font-weight: 700;
  border-radius: 50px;
  cursor: pointer;
  transition: all 0.3s ease;
  text-decoration: none;
  display: inline-block;
}

.btn-secondary:hover {
  background: rgba(164, 255, 61, 0.1);
  transform: translateY(-3px);
}
```

### 카드

#### Stat 카드

```css
.stat-card {
  background: linear-gradient(
    135deg,
    rgba(26, 29, 41, 0.6) 0%,
    rgba(15, 17, 23, 0.8) 100%
  );
  border: 1px solid rgba(164, 255, 61, 0.2);
  border-radius: 20px;
  padding: 2.5rem;
  text-align: center;
  transition: all 0.3s ease;
}

.stat-card:hover {
  transform: translateY(-10px);
  border-color: #a4ff3d;
  box-shadow: 0 0 40px rgba(164, 255, 61, 0.3);
}
```

#### Feature 카드

```css
.feature-card {
  background: linear-gradient(
    135deg,
    rgba(26, 29, 41, 0.5) 0%,
    rgba(15, 17, 23, 0.7) 100%
  );
  border: 1px solid rgba(164, 255, 61, 0.15);
  border-radius: 20px;
  padding: 2.5rem;
  display: flex;
  gap: 2rem;
  align-items: center;
  transition: all 0.4s ease;
}

.feature-card:hover {
  border-color: #a4ff3d;
  transform: translateX(10px);
  box-shadow: 0 20px 50px rgba(164, 255, 61, 0.2);
}
```

#### Summary 카드

```css
.summary-card {
  background: rgba(164, 255, 61, 0.05);
  border: 1px solid rgba(164, 255, 61, 0.2);
  border-radius: 15px;
  padding: 1.5rem;
  text-align: center;
}
```

### 입력 필드

```css
input[type="number"],
input[type="text"],
select {
  padding: 0.8rem 1rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(164, 255, 61, 0.2);
  border-radius: 10px;
  color: #ffffff;
  font-size: 1rem;
  font-family: 'Noto Sans KR', sans-serif;
  width: 100%;
  transition: all 0.3s ease;
}

input:focus,
select:focus {
  outline: none;
  border-color: #a4ff3d;
  box-shadow: 0 0 0 3px rgba(164, 255, 61, 0.1);
}

input:disabled,
input:read-only {
  background: rgba(255, 255, 255, 0.02);
  border-color: rgba(164, 255, 61, 0.1);
  color: #a0a3b5;
  cursor: not-allowed;
}
```

### FAQ 아이템

```css
.faq-item {
  background: linear-gradient(
    135deg,
    rgba(26, 29, 41, 0.5) 0%,
    rgba(15, 17, 23, 0.7) 100%
  );
  border: 1px solid rgba(164, 255, 61, 0.15);
  border-radius: 15px;
  margin-bottom: 1.5rem;
  overflow: hidden;
  transition: all 0.3s ease;
}

.faq-item.active {
  border-color: #a4ff3d;
}

.faq-question {
  padding: 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  cursor: pointer;
}

.faq-toggle {
  color: #a4ff3d;
  font-size: 1.5rem;
  transition: transform 0.3s ease;
}

.faq-item.active .faq-toggle {
  transform: rotate(45deg);
}

.faq-answer {
  padding: 0 2rem 2rem;
  display: none;
  animation: fadeIn 0.3s ease;
}

.faq-item.active .faq-answer {
  display: block;
}
```

### Solution Box

```css
.solution-box {
  background: linear-gradient(
    135deg,
    rgba(164, 255, 61, 0.1) 0%,
    rgba(143, 222, 53, 0.05) 100%
  );
  border: 2px solid #a4ff3d;
  border-radius: 20px;
  padding: 4rem;
  text-align: center;
  box-shadow: 0 20px 50px rgba(164, 255, 61, 0.15);
  max-width: 900px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .solution-box {
    padding: 2rem;
  }
}
```

---

## 애니메이션

### 트랜지션 타이밍

```css
/* 빠른 인터랙션 */
transition: all 0.3s ease;  /* 버튼, 호버 효과, 토글 */

/* 중간 트랜지션 */
transition: all 0.4s ease;  /* 카드 변형 */

/* 긴 트랜지션 */
transition: all 1s ease-out; /* 스크롤/진입 애니메이션 */

/* 배경/연속 애니메이션 */
animation: 3s - 20s;        /* 배경, shimmer */
```

### Keyframe 애니메이션

#### 1. fadeInUp (진입 효과)

```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

/* 사용 예시 */
.hero-content {
  animation: fadeInUp 1s ease-out;
}

/* 계단식 지연 */
.stat-card:nth-child(1) { animation-delay: 0s; }
.stat-card:nth-child(2) { animation-delay: 0.2s; }
.stat-card:nth-child(3) { animation-delay: 0.4s; }
```

#### 2. shimmer (텍스트 반짝임)

```css
@keyframes shimmer {
  to {
    background-position: 200% center;
  }
}

/* 사용 예시 */
.hero h1 {
  background: linear-gradient(
    90deg,
    #c5ff7a 0%,
    #a4ff3d 50%,
    #8fde35 100%
  );
  background-size: 200% auto;
  background-clip: text;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  animation: shimmer 3s linear infinite;
}
```

#### 3. float (배경 움직임)

```css
@keyframes float {
  0%, 100% {
    transform: translate(0, 0) rotate(0deg);
  }
  33% {
    transform: translate(30px, -30px) rotate(5deg);
  }
  66% {
    transform: translate(-20px, 20px) rotate(-5deg);
  }
}

/* 사용 예시 */
.bg-animation::before {
  animation: float 20s ease-in-out infinite;
}
```

#### 4. slideIn (슬라이드 진입)

```css
@keyframes slideIn {
  from {
    opacity: 0;
    transform: translateX(-30px);
  }
  to {
    opacity: 1;
    transform: translateX(0);
  }
}

/* 사용 예시 - 계단식 효과 */
.step:nth-child(1) {
  animation: slideIn 0.8s ease-out 0.2s forwards;
}
.step:nth-child(2) {
  animation: slideIn 0.8s ease-out 0.4s forwards;
}
.step:nth-child(3) {
  animation: slideIn 0.8s ease-out 0.6s forwards;
}
```

#### 5. float-icon (아이콘 부유)

```css
@keyframes float-icon {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}

/* 사용 예시 */
.risk-item-icon {
  animation: float-icon 3s ease-in-out infinite;
}
```

#### 6. fadeIn (단순 페이드)

```css
@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

/* 사용 예시 */
.faq-answer {
  animation: fadeIn 0.3s ease;
}
```

#### 7. spin (로딩 스피너)

```css
@keyframes spin {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}

/* 사용 예시 */
.spinner {
  animation: spin 1s linear infinite;
}
```

### 호버 효과 패턴

```css
/* 버튼 호버 - Y축 이동 + 그림자 증가 */
.btn:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(164, 255, 61, 0.5);
}

/* 카드 호버 - Y축 또는 X축 이동 + 테두리/그림자 */
.card:hover {
  transform: translateY(-10px);
  border-color: #a4ff3d;
  box-shadow: 0 0 40px rgba(164, 255, 61, 0.3);
}

/* 링크 호버 - 밑줄 확장 */
.nav-link::after {
  content: '';
  position: absolute;
  bottom: -5px;
  left: 0;
  width: 0;
  height: 2px;
  background: #a4ff3d;
  transition: width 0.3s ease;
}

.nav-link:hover::after {
  width: 100%;
}
```

---

## 레이아웃 시스템

### 그리드 패턴

```css
/* 반응형 자동 맞춤 그리드 */
.stats-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 2rem;
}

/* 설정 그리드 */
.settings-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
}
```

### 컨테이너 제약

```css
/* 최대 너비 제약 */
.container-sm { max-width: 700px; }   /* 리스크 콘텐츠 */
.container-md { max-width: 800px; }   /* Hero h2, 리스크 인트로 */
.container-base { max-width: 900px; } /* 기능, FAQ, solution box */
.container-lg { max-width: 1000px; }  /* 단계 */
.container-xl { max-width: 1200px; }  /* Hero, 통계, 메인 콘텐츠 */
.container-2xl { max-width: 1400px; } /* 시뮬레이터 */
```

### Flexbox 패턴

```css
/* 내비게이션 */
.nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

/* 버튼 그룹 */
.button-group {
  display: flex;
  gap: 1.5rem;
  justify-content: center;
  align-items: center;
}

/* 기능 카드 */
.feature-card {
  display: flex;
  gap: 2rem;
  align-items: center;
}

@media (max-width: 768px) {
  .feature-card {
    flex-direction: column;
    text-align: center;
  }
}

/* 단계 */
.steps {
  display: flex;
  flex-direction: column;
  gap: 3rem;
}
```

### 배경 레이어

```css
/* 메인 배경 */
body {
  background: radial-gradient(
    ellipse at top,
    #1a1d29 0%,
    #0f1117 50%
  );
  min-height: 100vh;
}

/* 애니메이션 배경 레이어 */
.bg-animation::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background:
    radial-gradient(
      circle at 20% 50%,
      rgba(164, 255, 61, 0.08) 0%,
      transparent 50%
    ),
    radial-gradient(
      circle at 80% 80%,
      rgba(164, 255, 61, 0.05) 0%,
      transparent 50%
    );
  animation: float 20s ease-in-out infinite;
  pointer-events: none;
}

/* 섹션별 배경 */
.how-it-works {
  background: linear-gradient(
    180deg,
    transparent 0%,
    rgba(26, 29, 41, 0.3) 100%
  );
}

.cta {
  background: radial-gradient(
    ellipse at center,
    rgba(164, 255, 61, 0.12) 0%,
    transparent 70%
  );
}
```

### 백드롭 효과

```css
/* 글래스모피즘 (내비게이션) */
nav {
  background: rgba(15, 17, 23, 0.9);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);
}
```

---

## 디자인 토큰

### 토큰 요약 테이블

| 토큰 유형 | 토큰 이름 | 값 | 사용처 |
|-----------|-----------|-----|--------|
| **컬러** | Primary | `#1a1d29`, `#0f1117` | 배경 |
| | Accent | `#a4ff3d`, `#8fde35`, `#c5ff7a` | 인터랙티브 요소 |
| | Text | `#ffffff`, `#a0a3b5` | 텍스트 색상 |
| | Error | `#ff6b6b`, `#ff4d4d` | 부정 상태 |
| **폰트** | Display | Orbitron (900, 700, 400) | 헤딩 |
| | Body | Noto Sans KR (700, 500, 400, 300) | 콘텐츠 |
| **크기** | XS | 0.9rem | 라벨 |
| | S | 1.1rem | 본문 텍스트 |
| | M | 1.6rem | 카드 제목 |
| | L | 3rem | 섹션 제목 |
| | XL | 4.5rem | 메인 헤딩 |
| **간격** | XS | 0.5rem | 타이트 간격 |
| | S | 1rem | 작은 간격 |
| | M | 2rem | 중간 간격 |
| | L | 3rem | 큰 간격 |
| | XL | 6rem | 섹션 간격 |
| **라운드** | Small | 10px | 입력 필드 |
| | Medium | 15px | FAQ 아이템 |
| | Large | 20px | 카드, 패널 |
| | Full | 50px | 버튼 |
| **그림자** | Glow | `0 0 40px rgba(164, 255, 61, 0.3)` | 강조 |
| | Elevation | `0 10px 30px rgba(164, 255, 61, 0.3)` | 깊이 |
| **트랜지션** | Quick | 0.3s | 호버 상태 |
| | Normal | 1s | 진입 애니메이션 |
| | Slow | 3s-20s | 배경 애니메이션 |

---

## 적용 가이드

### 1. CSS 변수 추출

새 프로젝트에서 `styles/variables.css` 파일 생성:

```css
:root {
  /* Colors */
  --primary-dark: #1a1d29;
  --primary-darker: #0f1117;
  --accent-green: #a4ff3d;
  --accent-green-dark: #8fde35;
  --accent-green-light: #c5ff7a;
  --text-light: #ffffff;
  --text-gray: #a0a3b5;

  /* Spacing */
  --spacing-xs: 0.5rem;
  --spacing-sm: 1rem;
  --spacing-md: 1.5rem;
  --spacing-lg: 2rem;
  --spacing-xl: 3rem;

  /* Typography */
  --font-display: 'Orbitron', sans-serif;
  --font-body: 'Noto Sans KR', sans-serif;

  /* Border Radius */
  --radius-sm: 10px;
  --radius-md: 15px;
  --radius-lg: 20px;
  --radius-full: 50px;

  /* Shadows */
  --shadow-glow: 0 0 40px rgba(164, 255, 61, 0.3);
  --shadow-elevation: 0 10px 30px rgba(164, 255, 61, 0.3);

  /* Transitions */
  --transition-quick: 0.3s ease;
  --transition-normal: 1s ease-out;
}
```

### 2. 컴포넌트 라이브러리 생성

`components/buttons.css`:

```css
.btn {
  padding: 1.2rem 3rem;
  font-size: 1.1rem;
  font-weight: 700;
  border-radius: var(--radius-full);
  cursor: pointer;
  transition: all var(--transition-quick);
  text-decoration: none;
  display: inline-block;
  border: none;
}

.btn-primary {
  background: linear-gradient(135deg, var(--accent-green) 0%, var(--accent-green-dark) 100%);
  color: var(--primary-darker);
  box-shadow: var(--shadow-elevation);
}

.btn-primary:hover {
  transform: translateY(-3px);
  box-shadow: 0 15px 40px rgba(164, 255, 61, 0.5);
}

.btn-secondary {
  background: transparent;
  color: var(--accent-green);
  border: 2px solid var(--accent-green);
}

.btn-secondary:hover {
  background: rgba(164, 255, 61, 0.1);
  transform: translateY(-3px);
}
```

`components/cards.css`:

```css
.card {
  background: linear-gradient(
    135deg,
    rgba(26, 29, 41, 0.5) 0%,
    rgba(15, 17, 23, 0.7) 100%
  );
  border: 1px solid rgba(164, 255, 61, 0.15);
  border-radius: var(--radius-lg);
  padding: var(--spacing-lg);
  transition: all var(--transition-quick);
}

.card:hover {
  border-color: var(--accent-green);
  box-shadow: var(--shadow-glow);
}

.card-stat {
  text-align: center;
}

.card-stat:hover {
  transform: translateY(-10px);
}

.card-feature {
  display: flex;
  gap: var(--spacing-lg);
  align-items: center;
}

.card-feature:hover {
  transform: translateX(10px);
}
```

### 3. 애니메이션 라이브러리

`animations/keyframes.css`:

```css
@keyframes fadeInUp {
  from {
    opacity: 0;
    transform: translateY(30px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes shimmer {
  to {
    background-position: 200% center;
  }
}

@keyframes float {
  0%, 100% { transform: translate(0, 0) rotate(0deg); }
  33% { transform: translate(30px, -30px) rotate(5deg); }
  66% { transform: translate(-20px, 20px) rotate(-5deg); }
}

/* 유틸리티 클래스 */
.animate-fade-in-up {
  animation: fadeInUp 1s ease-out;
}

.animate-shimmer {
  animation: shimmer 3s linear infinite;
}

.animate-float {
  animation: float 20s ease-in-out infinite;
}
```

### 4. 유틸리티 클래스

`utilities/spacing.css`:

```css
/* Margin */
.m-0 { margin: 0; }
.m-1 { margin: var(--spacing-xs); }
.m-2 { margin: var(--spacing-sm); }
.m-3 { margin: var(--spacing-md); }
.m-4 { margin: var(--spacing-lg); }

/* Padding */
.p-0 { padding: 0; }
.p-1 { padding: var(--spacing-xs); }
.p-2 { padding: var(--spacing-sm); }
.p-3 { padding: var(--spacing-md); }
.p-4 { padding: var(--spacing-lg); }

/* Gap */
.gap-1 { gap: var(--spacing-xs); }
.gap-2 { gap: var(--spacing-sm); }
.gap-3 { gap: var(--spacing-md); }
.gap-4 { gap: var(--spacing-lg); }
```

`utilities/text.css`:

```css
/* Typography */
.text-display {
  font-family: var(--font-display);
}

.text-body {
  font-family: var(--font-body);
}

.text-xs { font-size: 0.9rem; }
.text-sm { font-size: 1.1rem; }
.text-md { font-size: 1.6rem; }
.text-lg { font-size: 3rem; }
.text-xl { font-size: 4.5rem; }

/* Colors */
.text-light { color: var(--text-light); }
.text-gray { color: var(--text-gray); }
.text-accent { color: var(--accent-green); }

/* Weights */
.font-light { font-weight: 300; }
.font-normal { font-weight: 400; }
.font-medium { font-weight: 500; }
.font-bold { font-weight: 700; }
.font-black { font-weight: 900; }
```

### 5. 프로젝트 구조 예시

```
your-project/
├── styles/
│   ├── variables.css          # 디자인 토큰
│   ├── reset.css              # CSS 리셋
│   ├── base.css               # 기본 스타일
│   ├── components/
│   │   ├── buttons.css        # 버튼 컴포넌트
│   │   ├── cards.css          # 카드 컴포넌트
│   │   ├── forms.css          # 폼 요소
│   │   └── navigation.css     # 내비게이션
│   ├── animations/
│   │   └── keyframes.css      # 애니메이션 정의
│   ├── utilities/
│   │   ├── spacing.css        # 간격 유틸리티
│   │   ├── text.css           # 텍스트 유틸리티
│   │   └── layout.css         # 레이아웃 유틸리티
│   └── main.css               # 메인 임포트
```

### 6. 메인 CSS 임포트

`styles/main.css`:

```css
/* Google Fonts */
@import url('https://fonts.googleapis.com/css2?family=Orbitron:wght@400;700;900&family=Noto+Sans+KR:wght@300;400;500;700&display=swap');

/* Base */
@import './reset.css';
@import './variables.css';
@import './base.css';

/* Components */
@import './components/buttons.css';
@import './components/cards.css';
@import './components/forms.css';
@import './components/navigation.css';

/* Animations */
@import './animations/keyframes.css';

/* Utilities */
@import './utilities/spacing.css';
@import './utilities/text.css';
@import './utilities/layout.css';
```

### 7. 사용 예시

```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>새 프로젝트</title>
  <link rel="stylesheet" href="styles/main.css">
</head>
<body>
  <!-- 버튼 사용 -->
  <button class="btn btn-primary">시작하기</button>
  <button class="btn btn-secondary">더 알아보기</button>

  <!-- 카드 사용 -->
  <div class="card card-stat animate-fade-in-up">
    <h3 class="text-display text-lg text-accent">1,234</h3>
    <p class="text-body text-sm text-gray">총 사용자</p>
  </div>

  <!-- 기능 카드 -->
  <div class="card card-feature">
    <div class="feature-icon">
      <span>🚀</span>
    </div>
    <div class="feature-content">
      <h3 class="text-display text-md text-light">빠른 성능</h3>
      <p class="text-body text-sm text-gray">최적화된 속도로 빠르게 작동합니다.</p>
    </div>
  </div>
</body>
</html>
```

---

## 참고 파일

- **원본 디자인 시스템**: [index.html](index.html) (라인 10-707)
- **시뮬레이터 스타일**: [simulator.html](simulator.html) (라인 10-377)

---

## 라이선스 및 크레딧

이 디자인 시스템은 WebSea Landing 프로젝트에서 추출되었으며, 다른 프로젝트에 자유롭게 재사용할 수 있습니다.

**폰트 크레딧**:
- Orbitron - Google Fonts (Open Font License)
- Noto Sans KR - Google Fonts (Open Font License)

---

**문서 버전**: 1.0
**최종 업데이트**: 2025-12-12
