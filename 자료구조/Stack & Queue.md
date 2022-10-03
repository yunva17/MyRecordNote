# Stack

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FQLmgD%2FbtriadO71zj%2Fy3IaQwptHsuFd4dJjKOQBK%2Fimg.png)

- `LIFO(Last In Fisrt Out, 후입선출)`
- 가장 마지막으로 들어간 데이터가 가장 첫번째로 나오는 성질을 가진 자료구조
- 데이터를 제한적으로 접근할 수 있고 한쪽 끝에서만 자료를 넣거나 뺄 수 있는 구조
- 마지막으로 추가된 요소가 제일 먼저 제거됨
- 삽입 및 삭제에 O(1), 탐색에 O(N)이 걸림
- 가장 최근에 들어온 자료를 top이라고 하며 자료의 삽입과 삭제는 한 곳(top)에서만 이루어지게 됨

만약 스택이 비어있을 때 자료를 꺼내려고 시도를 하면 **스택 언더플로우(Stack Underflow)**가 발생하고
반대로, 스택이 꽉 차있을 때 자료를 넣으려고 하면 **스택 오버플로우(Stack Overflow)**가 발생하게 됩니다.

`장점`

- 구조가 단순해서 구현이 쉬움
- 데이터 저장/읽기 속도가 빠름

`단점`

- 데이터 최대 개수를 미리 정해야 함

- 파이썬의 경우 재귀 함수 호출은 1000번까지 가능함
- 저장 공간의 낭비가 발생할 수 있음
- 미리 최대 개수만큼 저장 공간을 확보해야 함

`스택의 활용 예시`

- 재귀적인 알고리즘
- 웹 브라우저 방문 기록(뒤로가기)
- 함수의 콜스택
- 문자열 역순 출력
- 연산자 후위표기법
- 컴퓨터 내부의 프로세스 구조의 함수 동작 방식
- 문서작업에서 Ctrl+Z

### 기본 구조

```
class Node {
    constructor(value){
        this.value = value;
        this.next = null;
    }
}

class Stack {
    constructor(){
        this.first = null;
        this.last = null;
        this.size = 0;
    }
}
```

### Push

- 데이터를 스택에 넣기 -> 노드를 리스트의 가장 앞에 추가

```
  push(val) {
    const newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      const temp = this.first;
      this.first = newNode;
      this.first.next = temp;
    }
    return ++this.size;
  }
```

### Pop

- 데이터(최상위 값)를 스택에서 꺼내기 -> 리스트의 가장 앞에 있는 노드를 제거

```
  pop() {
    if (!this.first) return null;
    const temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return temp.value;
  }
```

# Queue


![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FuXE7T%2Fbtrh94R1tqR%2FxQ5Ig2jbUlaEx0AZyVKTZK%2Fimg.png)

- `FIFO(First In First Out, 선입선출)`
- 먼저 집어넣은 데이터가 먼저 나오는 성질을 가진 자료구조
- 삽입 및 삭제에 O(1), 탐색에 O(N)이 걸림
- 큐의 가장 첫 원소를 front, 끝 원소를 rear라고 부름
- 들어올 때 rear로 들어오지만, 나올 때는 front부터 빠지는 특성을 가짐
- Rear부분에서 자료의 삽입이, Front부분에서 자료의 삭제가 이루어짐
- 접근방법은 가장 첫 원소와 끝 원소로만 가능

`큐의 활용 예시`

- CPU 작업을 기다리는 프로세스
- 스레드 행렬 또는 네트워크 접속을 기다리는 행렬
- 너비 우선 탐색
- 캐시
- 버퍼
- 너비 우선 탐색(BFS)
- 은행창구 번호표 대기
- 프린터 출력

### 기본 구조

- 데이터를 넣고 뺄 때 해당 값의 위치를 기억해야 함. (스택에서 스택 포인터와 같은 역할)
- 이 위치를 기억하고 있는 게 front와 rear
- front : deQueue 할 위치 기억
- rear : enQueue 할 위치 기억

```
class Node {
  constructor(value) {
    this.value = value;
    this.next = null;
  }
}

class Queue {
  constructor() {
    this.first = null;
    this.last = null;
    this.size = 0;
  }
}
```

### enQueue

- 큐에 데이터를 넣음(JS에서 push) -> push처럼 노드를 제일 뒤에 추가함 (시간복잡도 O(1))

```
  enqueue(val) {
    const newNode = new Node(val);
    if (!this.first) {
      this.first = newNode;
      this.last = newNode;
    } else {
      this.last.next = newNode;
      this.last = newNode;
    }
    return ++this.size;
  }
```

### deQueue

- 큐에서 데이터를 뺌(JS에서 shift) -> shift처럼 제일 앞 노드를 제거하고 반환함(시간복잡도 O(1))

```
  dequeue() {
    if (!this.first) return null;

    const temp = this.first;
    if (this.first === this.last) {
      this.last = null;
    }
    this.first = this.first.next;
    this.size--;
    return temp.value;
  }
```

일반 큐의 단점 : 큐에 빈 메모리가 남아 있어도, 꽉 차있는것으로 판단할 수도 있음
-> 이를 개선한 것이 '원형 큐', 논리적으로 배열의 처음과 끝이 연결되어 있는 것으로 간주함

### 원형큐

- 원형 큐는 초기 공백 상태일 때 front와 rear가 0
- 공백, 포화 상태를 쉽게 구분하기 위해 자리 하나를 항상 비워둠

원형 큐의 단점 : 메모리 공간은 잘 활용하지만, 배열로 구현되어 있기 때문에 큐의 크기가 제한
-> 이를 개선한 것이 '연결리스트 큐'
연결리스트 큐는 크기가 제한이 없고 삽입, 삭제가 편리

출처)
https://cocoon1787.tistory.com/691
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#stack-and-queue
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Stack%20%26%20Queue.md
https://ratsgo.github.io/data%20structure&algorithm/2017/10/15/queue/
https://ratsgo.github.io/data%20structure&algorithm/2017/10/11/stack/
https://github.com/junh0328/prepare_frontend_interview/blob/main/data_structure.md#%EC%8A%A4%ED%83%9D
https://velog.io/@jangws/15.-%EC%8A%A4%ED%83%9Dstack-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0-JS
