<b>
<ol>1. dfs는 사실 stack이 필요 없다. 재귀함수로 작성시 함수 호출 순서 자체가 function call stack에 쌓이기 때문이다. (물론 재귀함수 호출시마다 stack에
원소를 넣어서 방문 순서를 기록할수도 있다.)  </ol>
<ol>2. bfs는 queue에 push를 하는 순간, 방문하였다고 표시를 해줘야한다. queue에 push 하는 것과 방문체크를 다른 타이밍에 하게 되면, 방문한 vertex를
다시 방문하는 일이 발생한다.</ol>
<ol>  </ol>
<ol>  </ol>
<ol>  </ol>
<ol>  </ol>
</b>
