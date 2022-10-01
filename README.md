## Lecture-1

'프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1' 1번째 강의입니다.

### 요약

#### 1. 이미지 최적화
- img 태그는 본인의 width, height 픽셀의 2.4배정도 표현 할 수 있다. 
- 100x100 img 태그에 1200x1200 이미지를 사용하는건 낭비라는 뜻이다.
- imgix 같은 사이트를 사용해도 좋지만 이 강의에선 src 뒤에 파라미터로 `?w=${width}&h=${height}&q=${quality}&fm=${format}&fit=crop` 를 붙이면서 해결 했다.