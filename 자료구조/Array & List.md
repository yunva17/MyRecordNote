# 배열(Array)

- 같은 타입의 변수들로 이루어져 있고, 크기가 정해져 있으며, 인접한 메모리 위쳉 있는 데이터를 모아놓은 집합
- 논리적 저장 순서와 물리적 저장 순서가 일치하는 자료구조
- 중복을 허용하고 순서가 있음
- 초기에 배열의 크기를 지정해야 하며, 고정적이고 변경할 수 없음
- 인덱스로 해당 원소에 접근할 수 있으며 랜덤 접근(Random Access)이 가능 -> 탐색에 O(1)이 되어서
- 삽입/삭제 시 해당 원소에 접근하여 작업을 완료한 후 빈 공간이 생기지 않도록 shift 해줘야하므로 O(N) 소요
- 인덱스에 해당하는 원소를 빠르게 접근해야 하거나 간단하게 데이터를 쌓고 싶을 때 사용

`장점`

- 논리적 저장 순서 = 물리적 저장 순서
- 메모리 상에서 원소들이 연속적으로 붙어있어 인덱스 값을 이용하여 랜덤 접근이 가능

`단점`

- 데이터 삽입/삭제가 어려움
- 초기에 배열의 크기를 지정해야 하며, 고정적이고 변경할 수 없음

## 랜덤 접근(Random Access) vs 순차적 접근(Sequential Access)

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/a/a7/Random_vs_sequential_access.svg/1200px-Random_vs_sequential_access.svg.png)
(출처: 순차 접근 - 위키백과)

### 랜덤 접근

- 직접 접근.
- 동일한 시간에 배열과 같은 순차적인 데이터가 있을 때 임의의 인덱스에 해당하는 데이터에 접근할 수 있는 기능
- 데이터를 저장된 순서대로 검색해야 하는 순차적 접근과 반대

# List

- 데이터를 나열하고, 각 데이터를 인덱스에 대응하도록 구성한 데이터 구조
- 순서가 있고 중복을 허용함
- 인덱스로 원소에 접근이 가능
- 크기가 가변적임

`장점`

- 빠른 접근이 가능
- 첫 데이터의 위치에서 상대적인 위치로 데이터에 접근이 가능 (인덱스 번호로 접근 가능)

`단점`

- 데이터 삽입/삭제가 어려움

## ArrayList

![img](https://t1.daumcdn.net/cfile/tistory/995E66395B1CFD7D10)

- 단방향 포인터 구조로 데이터 순차적 접근에 강점을 가짐
- 배열을 기반으로 데이터를 저장
- index를 가짐
- Search는 빠르지만, 데이터 삽입/삭제가 느림

## 연결 리스트(LinkedList)

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png)
(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

- 양방향 포인터 구조 -> 떨어진 곳에 존재하는 데이터를 화살표로 연결해서 관리
- 데이터의 삽입 및 삭제가 빠름 -> O(N)
- 단, 삽입, 삭제하려는 데이터의 위치가 맨 앞 혹은 맨 뒤 일 경우 시간 복잡도가 O(1)이 될 수 있음
- 검색의 경우 시간 복잡도 O(N)
- 각각의 원소들은 자기 자신 다음에 어떤 원소인지 기억함
- 원하는 위치에 삽입 할때 search 과정에서 첫번째 원소부터 다 확인해야 함
- 논리적 저장 순서 != 물리적 저장 순서
- Tree 구조의 근간이 되는 자료구조

> 단일은 뒤에 노드만 가리키고, 다중은 앞뒤 노드를 모두 가리킴

### 기본 구조와 용어

- 노드(Node): 데이터 저장 단위 (데이터값, 포인터) 로 구성
- 포인터(pointer): 각 노드 안에서, 다음이나 이전의 노드와의 연결 정보를 가지고 있는 공간

`장점`

- 데이터 삽입/삭제가 빠름
- 필요할 때 크기를 늘리거나 줄일 수 있어 메모리 관리가 효율적(동적으로 크기가 늘어남)
- 연속된 메모리 공간이 필요 없음
- 미리 데이터 공간을 할당하지 않아도 됨

`단점`

- 메모리 연속성을 가지지 않기 때문에 랜덤 접근(Random Access)이 불가능
- 검색 시 처음 노드부터 순차적으로 순회해야 함
- 연결을 위한 별도 데이터 공간이 필요하므로, 저장 공간 효율이 높지 않음
- 중간 데이터 삭제시, 앞뒤 데이터의 연결을 재구성해야 하는 부가적인 작업 필요

## Doubly linked list

![img](https://upload.wikimedia.org/wikipedia/commons/thumb/6/6d/Singly-linked-list.svg/408px-Singly-linked-list.svg.png)
(출처: wikipedia, https://en.wikipedia.org/wiki/Linked_list)

- 앞 뒤 방향 모두 노드 탐색이 가능함
- 이중 연결 리스트라고도 함

`장점`

- 양방향으로 연결되어 있어 노드 탐색이 양쪽 모두 가능

## 배열과 리스트 비교

- array는 선언할 때 크기오 데이터 타입을 지정 / List는 array처럼 크기를 정해주지 않아도 됨
- array는 index가 중요 / List에서는 순서가 중요

> array나 arrayList에서는 index를 가지고 있기 때문에 검색이 빠르지만
> LinkedList는 처음부터 살펴봐야해서(순차) 검색이 느림

| /                   | Array | ArrayList | LinkedList |
| ------------------- | :---: | :-------: | :--------: |
| 랜덤 접근           | 가능  |   가능    |   불가능   |
| 탐색                | 빠름  |   빠름    |    느림    |
| 데이터 삽입 및 삭제 | 느림  |   느림    |    빠름    |

출처
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#array-vs-linked-list
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Array%20vs%20ArrayList%20vs%20LinkedList.md
https://github.com/junh0328/prepare_frontend_interview/blob/main/data_structure.md#%EB%A6%AC%EC%8A%A4%ED%8A%B8
https://cocoon1787.tistory.com/527
https://cocoon1787.tistory.com/705
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Linked%20List.md
