<b>1. stack 과 queue 사용에 있어서, 
<ul>-1. pop 전에 컨테이너안에 원소가 들어있는지 부터 체크하고 pop 할 것.</ul>
<ul>-2. 컴파일러 별로 내가 stack이나 queue를 선언했더라도, 코드중간에 해당 컨테이너의 원소개수가 0개라고 메모리 해제 해버리는경우가 있으니,
조심히 잘 살펴보자.</ul> </b>

```c++
#include <iostream>
#include <queue>
using namespace std;
queue<int> qu;
vector<int> list[15];
int check[15] = {0};

void bfs(int idx);

int main() {
  list[1].push_back(6);
  list[6].push_back(1);

  list[1].push_back(5);
  list[5].push_back(1);

  list[6].push_back(4);
  list[4].push_back(6);

  list[10].push_back(6);
  list[6].push_back(10);

  list[5].push_back(3);
  list[3].push_back(5);

  list[3].push_back(7);
  list[7].push_back(3);

  list[3].push_back(8);
  list[8].push_back(3);

  list[4].push_back(2);
  list[2].push_back(4);

  list[2].push_back(9);
  list[9].push_back(2);

  check[1] = 1;
  qu.push(1);
  bfs(1);

  int size = qu.size();

  for(int i=0; i<size; i++){
    printf("%d ",qu.front());
    qu.pop();
  }
}

void bfs(int idx){
  vector<int> :: iterator it;
  int next;
  
  cout << idx << endl;

  for(it = list[idx].begin(); it != list[idx].end(); it++){
    if(check[*it] == 0){
      check[*it] = 1;
      qu.push(*it);
    }
  }
  if(!qu.empty()){///////////////////// 이 조건문을 생략했다면?
    qu.pop();
    next = qu.front();
    bfs(next);
  }
  return;
}
```

여기에서 

```c++
if(!qu.empty()){/////////////////////
    qu.pop();
    next = qu.front();
    bfs(next);
  }
```

이 조건문을 생략했다면, bfs가 끝나고도 원소가 없는 queue에서 지속적으로 원소를 뽑아내려 하기 때문에 runtime error 봉착 하게 될것. <br>
<b>주의</b>
