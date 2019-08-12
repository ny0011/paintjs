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
