# SEO 설정 가이드

SIPE 4번째 사담콘 랜딩 페이지에 구글 검색 최적화(SEO)를 위한 설정이 완료되었습니다.

## 적용된 SEO 최적화 사항

### 1. 기본 메타 태그
- 제목, 설명, 키워드 최적화
- 검색 로봇 허용 설정
- Canonical URL 설정

### 2. 소셜 미디어 최적화 (Open Graph)
- Facebook, Twitter 카드 지원
- 공유 시 표시될 이미지, 제목, 설명 설정

### 3. 구조화된 데이터 (JSON-LD)
- Schema.org Event 마크업 적용
- 검색 결과에서 리치 스니펫 표시 가능

### 4. 검색 엔진 최적화 파일
- `robots.txt`: 검색 로봇 크롤링 규칙
- `sitemap.xml`: 사이트 구조 정보
- `site.webmanifest`: PWA 지원

### 5. 기술적 SEO
- 모바일 친화적 설정
- 페이지 로딩 속도 최적화
- 의미론적 HTML 구조

## 추가 설정 필요 사항

### 1. Open Graph 이미지 생성
현재 `/public/og-image-placeholder.md` 파일을 실제 이미지로 교체해야 합니다:
- 파일명: `og-image.jpg`
- 크기: 1200x630px
- 내용: SIPE 로고, 이벤트 제목, 날짜 정보

### 2. Google Analytics/Tag Manager 설정
`index.html`에서 주석 처리된 부분을 활성화하고 실제 ID로 교체:
```html
<!-- GTM-XXXXXXX를 실제 Google Tag Manager ID로 교체 -->
<script>(function(w,d,s,l,i){...})(window,document,'script','dataLayer','GTM-YOUR-ID');</script>
```

### 3. Google Search Console 인증
`index.html`에서 인증 메타 태그 활성화:
```html
<!-- your-verification-code-here를 실제 인증 코드로 교체 -->
<meta name="google-site-verification" content="your-verification-code-here" />
```

### 4. 파비콘 생성
다음 아이콘 파일들을 `/public/` 폴더에 추가:
- `favicon-16x16.png`
- `favicon-32x32.png`
- `apple-touch-icon.png` (180x180px)
- `android-chrome-192x192.png`
- `android-chrome-512x512.png`

### 5. 도메인 URL 업데이트
현재 `https://sipe-4th-sadamcon.com`으로 설정된 URL을 실제 도메인으로 변경:
- `index.html`의 canonical URL
- `sitemap.xml`의 URL
- Open Graph URL
- 구조화된 데이터의 URL

## SEO 체크리스트

배포 전 확인사항:
- [ ] Open Graph 이미지 생성 및 업로드
- [ ] 실제 도메인 URL로 모든 링크 업데이트
- [ ] Google Analytics/Tag Manager ID 설정
- [ ] Google Search Console 인증
- [ ] 파비콘 파일들 업로드
- [ ] 사이트맵 제출 (Google Search Console)
- [ ] 페이지 속도 테스트 (PageSpeed Insights)
- [ ] 모바일 친화성 테스트 (Mobile-Friendly Test)

## 추천 SEO 도구

1. **Google Search Console**: 검색 성능 모니터링
2. **Google Analytics**: 방문자 분석
3. **PageSpeed Insights**: 페이지 속도 측정
4. **Mobile-Friendly Test**: 모바일 최적화 확인
5. **Rich Results Test**: 구조화된 데이터 검증
