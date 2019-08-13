# paintjs

Painting Board made with VanilaJS

### 화면 끝

### JS 편집ㄱㄱ

#### 1. 캔버스 위에 마우스를 클릭하면서 움직일 때 선 그리기

-   캔버스 위에서 마우스를 움직임 => event이름: mousemove
-   console.log로 값을 확인해보면 여러 정보들이 나옴.
-   clientX,Y는 전체 화면(body)에서의 마우스 위치고 offsetX,Y가 캔버스 태그 안에
    서의 마우스 위치임
-   캔버스 위에서 클릭했을 때 선이 그어지게 하고 싶음 => event이름: mousedown
-   마우스 클릭을 뗐을 때 선이 멈추고 싶음 => event이름: mouseup
-   마우스가 캔버스를 벗어나면 그리는 것을 멈추고 싶음 => event이름: mouseleave

-   canvas API를 알아보자 : 그림을 그릴 수 있음
    (https://developer.mozilla.org/ko/docs/Web/HTML/Canvas)
-   canvas 객체의 context에 접근하면 context가 pixel을 변경시킬 수 있음.
-   const context = document.getElementById('canvas').getContext('2d'); : 2d용
    context를 얻음. context는 canvas 태그 사이에 있는 pixel에 접근하게 됨.
    (<canvas> context </canvas>)
-   선 그리기 : canvas의 path 참조
    (https://developer.mozilla.org/ko/docs/Web/HTML/Canvas/Tutorial/Drawing_shapes#%EA%B2%BD%EB%A1%9C_%EA%B7%B8%EB%A6%AC%EA%B8%B0)
-   1. beginPath()로 경로 생성(시작점 지정)
-   2. moveTo()로 시작점 위치 옮김
-   3. lineTo(x,y)로 현재 path 시작점에서 (x,y) 끝점까지 직선을 그린다
-   하지만 그려지지 않았다!
