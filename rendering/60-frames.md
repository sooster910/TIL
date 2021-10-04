### To render 60 frames every 1000s, how much time is available to render a single frame?

1000ms/60fps = ~16ms

즉 60fps를 유지하기 위해선 한 프레임당 16 ms 이내로 유지해야 한다.

devtools - parse html

recalculate styles : dom+css 를 작업한다
이렇게 작업하고 나면 새로운 tree를 갖게 되는데 그것이 render tree이다.

render tree 는 dom과 비슷하긴 하지만 다르다.

redner tree는 <head>태그, <script>태그가 없다.
css요소들이 render tree에 추가 되고

only elements that will actually be displayed on the page will make it into the render tree.

critical rendering path

render tree는 오직 visible한 속성만 가지고 있다. 4개의 스타일중에 render tree에 존재하지 않는것은 어떤 것일까?

1. .style1{display:none;}
2. .style2::before{display:block;}
3. .style3{height:0;}
4. .style4{position:absolute; left:100%;}

정답은 1번이다. 나머지는 페이지 상에 보이진 않지만 여전히 페이지의 한부분으로 존재한다. display:none 은 element자체를 rendering하지 않는다. 그렇기 때문에 render tree에 포함되지 않는다.
