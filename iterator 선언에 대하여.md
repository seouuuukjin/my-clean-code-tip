<b>1. 다양한 함수에서 동일하게 사용한다고 무조건 전역변수로 선언하지 말것.</b>

ex)

```c++
#include <iostream>
#include <stack>
#include<vector>
#include <string.h>
using namespace std;

int check[10] = {0};
vector <int> list[15];
stack<int> st;

//vector<int> :: iterator it;

void dfs(int idx){
   vector<int> :: iterator it; //반복자는 해당 함수 안에 생성하자.
   //어차피 모든 함수에서 반복자 다 사용한다고 전역으로 선언하면,
   //재귀 함수 사용시에 무조건 꼬인다.
   
  check[idx] = 1;
  cout << "idx = " <<idx << endl;

  for(it = list[idx].begin(); it != list[idx].end(); it++){
    if(check[*it] == 0){
      st.push(*it);
      dfs(*it);
    }
  }
}

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
  st.push(1);
  dfs(1); 
  for(int i=0; i<st.size(); i++){ ///////////////
    printf("#%d ", st.top());
    st.pop();
  }
  return 0;
}
```
다양한 함수에서 동일하게 사용한다고 무조건 전역변수로 선언하지 말것.

```
//vector<int> :: iterator it;
```
이렇게 전역 변수로 선언하지 말고,

```
void dfs(int idx){
   vector<int> :: iterator it; ////////////////////
```
반복자는 해당 함수 안에 생성하자.
어차피 모든 함수에서 반복자 다 사용한다고 전역으로 선언하면,
재귀 함수 사용시에 무조건 꼬인다.
<p><p>
<b>2. 반복문 작성시에 종료조건에 비교하는 두번째 항에 상수를 넣자. (내가 생각하기에 상수라고 보여도 다시한번 보자.)</b>
```
for(int i=0; i<st.size(); i++){ ///////////////
    printf("#%d ", st.top());
    st.pop();
  }
```
스택 사이즈는 원래 10이었지만, 반복문 안에서 지속적으로 pop을 해주고 있으므로, size()함수의 값은 계속 바뀐다.
```
for(int i=0; i<10; i++){ /////dfs여서 vertex 개수만큼 반복한다. 변수로 작성원할시에는 초기에 stack size 저장해둬서 사용하기
    printf("#%d ", st.top());
    st.pop();
  }
```
<b>주의</b>
