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
 
#### 4. 텍스트 압축
- cra에서 기본적으로 텍스트 압축을 해준다. pakege.json의 script에서 -u 옵션을 추가해주면 텍스트 압축을 끌 수 있다.
- 텍스트 압축이 마냥 좋지만은 않다. 압축 -> 압축해제에 시간이 걸리기 때문
- 개발자 도구의 network 탭에서 용량을 확인했을 때 2kb 이상의 파일들은 압축을 하는게 더 좋다.
- 확인해보면 168kb -> 48kb로 약 1/5정도로 용량이 줄은걸 확인했다.

## Lecture-2

'프론트엔드 개발자를 위한, 실전 웹 성능 최적화(feat. React) - Part. 1' 2번째 강의입니다.

### 요약

#### 1. 애니메이션 최적화
- ```width: ${({width}) => width}%;``` 이런식의 동적인 width값을 주는것 보다는 (width, heigh, top 등등은 reflow가 발생한다.)
- ```transform: scaleX(${({ width }) => width / 100});``` 이런식으로 transform을 활용하면 reflow, repaint를 피할 수 있다.
- 또한 gpu의 도움을 약간아니마 받기때문에 성능에도 도움이 된다. 이러한 이유들로 애니매이션의 프레임을 일정하게 유지하여 버벅임을 피할 수 있다.


#### 2. 컴포넌트 lazy loading
- 1강에서 배웠던 내용과 동일하기에 pass

#### 3. 컴포넌트 preloading
- 어떠한 모달이나 새 컴포넌트를 띄울때 ```const component = import("./components/ImageModal");``` 이러한 함수를 onMouseEnter 에 넣게되면 버튼을 누르기 전에 컴포넌트가 로딩되기 때문에 버튼을 눌렀을때 빠르게 뜨며 사용자 경험이 좋아진다. 컴포넌트가 너무 커 1초로 부족하다면 Page가 didmount 되었을 때 로드 하는 방법도 있다. 

### 4. 이미지 preloading
- 이미지를 미리 로딩하여 클릭하자마자 바로 뜰 수 있게 준비하는 방법이다. 그러나 너무 많은 이미지를 preload하면 성능에 저하가 있을 수 있어 중요한 이미지만 하는것이 좋다