## Lecture-1

'프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1' 1번째 강의입니다.

### 요약

#### 1. 이미지 최적화
- img 태그는 본인의 width, height 픽셀의 2.4배정도 표현 할 수 있다. 
- 100x100 img 태그에 1200x1200 이미지를 사용하는건 낭비라는 뜻이다.
- imgix 같은 사이트를 사용해도 좋지만 이 강의에선 src 뒤에 파라미터로 `?w=${width}&h=${height}&q=${quality}&fm=${format}&fit=crop` 를 붙이면서 해결 했다.

#### 2. 자바스크립트 실행시간 줄이기
- 개발자도구 -> 성능탭으로 가면 프로파일링 시작 이라는 버튼으로 성능을 볼 수 있다.
- 탭에 나와있는 결과중 비정상적으로 긴 실행시간을 가지고있는 컴포넌트가 있을 수 있다.
- 해당 컴포넌트에 들어가서 for, while 같은 로직을 간단하게 바꿈으로써 Light House 점수가 14점 오른걸 확인하였다.
- 자바스크립트 파일을 분석하려면 webpack에서는 webpack bundle analyzer을 사용해서 할수있고 CRA 에서는 cra bundle analyzer 을 사용할 수 있다.

#### 3. 코드 스플릿, lazy loading
- cra bundle analyzer을 참고하면 페이지에서 필요없는 자바스크립트를 사용하기 때문에 성능이 저하되는걸 볼 수 있음
- route-based code splitting (https://reactjs.org/docs/code-splitting.html)으로 해결 가능함
- webpack에서는 따로 설정을 해야한다. (https://webpack.js.org/guides/code-splitting/)
- lazy,Suspense를 적용하고 다시 cra bundle analyzer를 실행하면 필요한 부분만 분리되서 적용되는걸 확인 가능하다.
 
