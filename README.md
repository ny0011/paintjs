# paintjs

Painting Board made with VanilaJS

### 화면 끝

### JS 편집ㄱㄱ

#### 1. 캔버스 위에 마우스를 클릭하면서 움직일 때 선 그리기

- 캔버스 위에서 마우스를 움직임 => event이름: mousemove
- console.log로 값을 확인해보면 여러 정보들이 나옴.
- clientX,Y는 전체 화면(body)에서의 마우스 위치고 offsetX,Y가 캔버스 태그 안에
  서의 마우스 위치임
- 캔버스 위에서 클릭했을 때 선이 그어지게 하고 싶음 => event이름: mousedown
- 마우스 클릭을 뗐을 때 선이 멈추고 싶음 => event이름: mouseup
- 마우스가 캔버스를 벗어나면 그리는 것을 멈추고 싶음 => event이름: mouseleave

- **canvas API를 알아보자 : 그림을 그릴 수 있음**
  (https://developer.mozilla.org/ko/docs/Web/HTML/Canvas)
- canvas 객체의 context에 접근하면 context가 pixel을 변경시킬 수 있음.
- const context = document.getElementById('canvas').getContext('2d'); : 2d용
  context를 얻음. context는 canvas 태그 사이에 있는 pixel에 접근하게 됨.
  (<canvas> context </canvas>)
- 선 그리기 : canvas의 path 참조. path는 line이다!
  (https://developer.mozilla.org/ko/docs/Web/HTML/Canvas/Tutorial/Drawing_shapes#%EA%B2%BD%EB%A1%9C_%EA%B7%B8%EB%A6%AC%EA%B8%B0)
- 1. beginPath()로 경로 생성(시작점(0,0) 지정)
- 2. moveTo(a,b)로 시작점 위치 옮김
- 3-1. lineTo(x1,y1)로 이전 path의 시작점(a,b)에서 (x1,y1) 끝점을 잇는 직선을
  만든다(눈에 안보임)
- 4-1. stroke()로 실제로 획을 긋는다(눈에 보임)
- 3-2. lineTo(x2,y2)로 이전 path의 시작점(x1, y1)에서 (x2,y2) 를 잇는 직선을만
  든다
- 4-2. stroke()로 실제로 획을 긋는다(눈에 보임)
- (5. closePath()를 하면 lineTo(x',y')를 기준으로 (x',y') -> (a,b)로 연결되는
  직선이 생성된다. 시작점이 고정되고 마우스가 움직인 궤적을 끝점으로 하는 직선
  이 생김)
- 하지만 그려지지 않았다!

- **canvas의 특성 때문임.**
  (https://stackoverflow.com/questions/43853119/javascript-wrong-mouse-position-when-drawing-on-canvas)
- canvas는 두가지 size 특성을 가짐
- 1. pixel에서의 해상도 (canvas.width, canvas.height, 숫자값)
- 2. CSS에서 canvas보여줄 때 화면 크기(canvas.style.width,
     canvas.style.height, 문자열. "100%", "100px" 등으로 표기)
- 이 두가지는 연관있지 않고 독립적임.
- 기본적으로 canvas 해상도는 width=300, height=150 으로 되어 있음.

- **선의 색을 바꿔보자**
- 원형으로 만든 색칠된 div의 class를 jsColor로 주고 그 class에 해당하는 객체를
  받아서 출력해보니 HTMLCollection 객체들로 나옴.
- -> 객체들을 배열의 원소로 묶어보자 : Array.from()
  (https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
- 배열의 각 원소에 접근할 때 : forEach()
- Array.from(colors).forEach(color => color.addEventListener("click",
  handleColorClick)) : 원소의 이름을 color로 함, => 옆에는 각 원소(color) 가할
  행동(함수)을 써주면 됨.
- handleColorClick 함수에서 console.log(event.target.style); 를 찍으면
  CSSStyleDeclaration 이라는 객체를 리턴 받음. 얘는 CSS로 정의한 요소들을 다갖
  고 있는가봄

- **선 두께를 바꿔보자**
- range가 input tag니까 range를 움직이면 event listener는 input 이벤트를 받음
  (addEventListener("input", handleRangeChange))
- event에서 변경된 값은 input 태그의 value에 저장돼 있음 => event.target.value

- **fill 버튼을 누르면 paint 버튼, paint 버튼을 누르면 fill 버튼으로 바뀌게 하자**
- fill 버튼을 누르면 paint버튼으로 변경 하고 canvas를 클릭했을 때 canvas에 색
  칠되도록 한다. -> ctx.fillRect(x,y,width,height)
- fill 상태인지 아닌지를 확인하기 위한 변수 filling을 만들자

- **저장 버튼을 누르면 캔버스 이미지를 저장하자**
- 캔버스의 이미지를 저장하면 배경이 투명함. html속성만 정해주고 canvas 배경을 안막아줘서 그런가봄(??)
- 우클릭하면 캔버스 이미지를 다운로드를 할 수 있는데 그 이벤트를 막고 싶음 -> 우클릭 이벤트 : contextMenu, event.preventDefault()

- 캔버스를 이미지로 바꾸고 그 이미지를 저장한다
- -> HTMLCanvasElement.toDataURL() : console.log로 찍어서 나오는 값들이 모두 이미지임.
- link의 href에 toDataURL()을 넣어주고 download에는 파일 이름을 준다
- a태그를 눌러서 다른 페이지로 이동하니까 a태그를 눌러서 다운로드 받게 하면 됨. a태그를 클릭하자! -> link.click()
- https://developer.mozilla.org/en-US/docs/Web/HTML/Element/a#Using_the_download_attribute_to_save_a_%3Ccanvas%3E_as_a_PNG
