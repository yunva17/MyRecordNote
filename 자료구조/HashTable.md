# HashTable


- 키(Key)에 데이터(Value)를 저장하는 데이터 구조
- 해시함수를 사용하여 키를 해시값으로 매핑하고, 이 해시값을 색인(index) 혹은 주소 삼아 데이터의 값(value)을 키와 함께 저장하는 자료구조
- 보통 배열로 미리 HashTable 사이즈만큼 생성 후에 사용
- 작은 크기의 캐시 메모리로도 프로세스를 관리하도록 할 수 있음
- 삽입, 삭제, 탐색 시 평균적으로 `O(1)`의 시간 복잡도를 가짐
- Key를 통해 바로 데이터를 받아올 수 있으므로 속도가 빨라짐
- JS의 경우 별도로 구현할 필요가 없음 -> 객체 타입 { key: 'value' } 을 제공하기 때문

![img](https://camo.githubusercontent.com/08d8e874f0763db13897d3e8e02ae6f7f2931c2c2565a0b1cb4a1143c634cbb6/68747470733a2f2f7777772e66756e2d636f64696e672e6f72672f30305f496d616765732f686173682e706e67)

![img](https://velog.velcdn.com/post-images%2Fcyranocoding%2F8d25f580-b225-11e9-a4ce-730fc6b3757a%2F1iHTnDFd3sR5FqjHD1FDu9A.png)

## 기본 용어

- 해싱(Hashing) : 매핑하는 과정
- 키(Key) : 매핑 전 원래 데이터의 값, 고유한 값이며 해시 함수의 input, 해시함수(hash function)를 통해 해시(hash)로 변경이 되며 해시는 값(value)과 매칭되어 저장소에 저장됨
- 해시값(Hash value) : 매핑 후 데이터의 값, 저장소(bucket, slot)에 최종적으로 저장되는 값
- 해시 테이블(Hash Table): 키 값의 연산에 의해 직접 접근이 가능한 데이터 구조
- 해시함수(hash function) :
  데이터의 효율적 관리를 목적으로 임의의 길이의 데이터를 고정된 길이의 데이터로 매핑하는 함수 => 키(key)를 해시(hash)로 바꿔주는 역할
  Key를 해시 함수로 연산해서 해시 값을 알아내고, 이를 기반으로 해시 테이블에서 해당 key에 대하 데이터 위치를 일관성 있게 찾을 수 있음

`장점`

- 데이터 저장/읽기 속도가 빠름(검색 속도가 빠름)
- 키에 대한 데이터가 있는지(중복) 확인이 쉬움
- 키를 바탕으로 한 데이터의 유무를 파악하기 쉬움
- 적은 리소스로 많은 데이터를 효율적으로 관리할 수 있음
- 모든 데이터를 살피지 않아도 검색과 삽입/삭제가 빠름 -> 색인(index)에 해시값을 사용하기 때문
- 키와 해시값 사이에 직접적인 연관이 없기 때문에 해시값을 가지고 키를 완전히 복원하기 어려움

`단점`

- 일반적으로 저장공간이 더 많이 필요함
- 여러 키에 해당하는 주소가 동일할 경우 충돌을 해결하기 위한 별도 자료구조가 필요
- 해시 함수를 통해 나눠져 저장되는 해쉬 테이블의 주소가 같은데, 별도의 처리를 하지 않을 경우 키를 바탕으로 한 데이터가 덮어씌워질 가능성이 있음
- 중복이 일어나지 않도록 해시 테이블의 공간을 넓게 설계해야 함

`이럴 때 사용!!`

- 검색이 많이 필요한 경우
- 저장, 삭제, 읽기가 빈번한 경우

## 해시 충돌(Hash Collision)

- 해시함수는 해시값의 개수보다 대개 많은 키값을 해시값으로 변환(many-to-one 대응)하기 때문에 해시함수가 서로 다른 두 개의 키에 대해 동일한 해시값을 내는 해시충돌(collision)이 발생하게 됨
  ![img](https://i.imgur.com/NnEBDcX.png)

- 해시 충돌이 하나도 없는 해시 함수를 만드는 것은 불가능
- 해시 충돌이 발생하는 근본적인 원인은 비둘기집 원리

### 적재율

- 해시 테이블의 크기에 대한 키의 개수의 비율
  키의 개수를 K, 해시 테이블의 크기를 N이라고 했을 때 적재율은 K/N
- 충돌이 발생하지 않을 경우 해시 테이블의 탐색, 삽입, 삭제 연산은 모두 `O(1)`에 실행되지만,
  충돌이 발생할 경우에는 탐색과 삭제 연산이 `O(K)`만큼 걸림

> 따라서 해시 테이블의 충돌을 완화하는 방향으로 문제를 보완해야 함

## 해시 충돌 해결

![img](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FCoiPf%2Fbtq2qyoJVrN%2FERiH4UbKnKHQyF4R0HGjOk%2Fimg.png)
출처(https://st-lab.tistory.com/240?category=856997)

### open addressing(개방 주소법)

---

- 해시 충돌이 발생하면, (즉 삽입하려는 해시 버킷이 이미 사용 중인 경우) **다른 해시 버킷에 해당 자료를 삽입하는 방식**
- 해시 함수로 얻은 주소가 아닌, 다른 주소에 데이터를 저장할 수 있도록 허용하는 것
- 부하율(load factor)이 높을 수록(= 테이블에 저장된 데이터의 밀도가 높을수록) 성능이 급격히 저하됨

`장점`

- 또 다른 저장공간 없이 해시테이블 내에서 데이터 저장 및 처리가 가능
- 또 다른 저장공간에서의 추가적인 작업이 없음

`단점`

- 해시 함수(Hash Function)의 성능에 전체 해시테이블의 성능이 좌지우지됨
- 데이터의 길이가 늘어나면 그에 해당하는 저장소를 마련해 두어야 함

#### 1. 선형 탐사법(Linear Probing)

- 간단하게 선형으로 **순차적** 검색을 하는 방법
- 시 함수로 나온 해시 index에 이미 다른 값이 저장되어 있다면, 해당 해시값에서 고정 폭을 옮겨 다음 해시값에 해당하는 버킷에 액세스함
- 특정 해시 값의 주변이 모두 채워져 있는 일차 군집화(primary clustering) 문제에 취약함

> 해시 충돌이 해시 값 전체에 균등하게 발생할 때 유용한 방법

#### 2. 제곱 탐사법(Quadratic Probing)

- 2차 함수를 이용해 탐색할 위치를 찾음
- 고정 폭으로 이동하는 선형 탐사와 달리 그 폭이 **제곱수**로 늘어남
- 데이터의 밀집도가 선형 탐사법보다 낮기 때문에 다른 해시값까지 영향을 받아서 연쇄적으로 충돌이 발생할 가능성이 적음
- 선형 탐사법 보다는 캐시의 성능이 떨어져서 속도의 문제가 발생함

#### 3. 이중 해싱(Double Hashing)

- 탐사할 해시값의 규칙값을 없애서 클러스터링을 방지
- 즉 해시 함수를 이중으로 사용하는데, 하나는 최초의 해시값을 얻을 때, 다른 하나는 해시 충돌이 일어났을 때 탐사 이동폭을 얻기 위해 사용
- 하나의 해쉬 함수에서 충돌이 발생하면 2 차 해쉬 함수를 이용해 새로운 주소를 할당함
- 위 두 가지 방법에 비해 많은 연산량을 요구하게 됨

> 최초 해시값이 같더라도 탐사 이동폭이 달라지고, 탐사 이동폭이 같더라도 최초 해시값이 달라져 위의 두 방법을 모두 완화할 수 있음

### seperate chaining(분리 연결법)

- 개방 주소법과는 달리 한 버킷(슬롯) 당 들어갈 수 있는 엔트리의 수에 제한을 두지 않음 -> 모든 자료를 해시테이블에 담는 것
- 이때 버킷에는 연결 리스트(linked list)나 트리(tree)를 사용함
- 해당 버킷에 데이터가 이미 있다면 체인처럼 노드를 추가하여 다음 노드를 가리키는 방식으로 구현

`장점`

- 해시 충돌이 일어나더라도 연결 리스트로 노드가 연결되기 때문에 index가 변하지 않고 데이터 개수의 제약이 없음
- 한정된 저장소(Bucket)을 효율적으로 사용할 수 있음
- 해시 함수(Hash Function)을 선택하는 중요성이 상대적으로 적음
- 상대적으로 적은 메모리를 사용하며 미리 공간을 잡아 놓을 필요가 없음

`단점`

- 한 Hash에 자료들이 계속 연결된다면(쏠림 현상) 검색 효율을 낮출 수 있음
- 외부 저장 공간을 사용함
- 외부 저장 공간 작업을 추가로 해야 함

`연결 리스트를 사용하는 방식(Linked List)`

- 각각의 버킷(bucket)들을 연결리스트(Linked List)로 만들어 Collision 이 발생하면 해당 bucket 의 list 에 추가하는 방식
- 연결 리스트의 특징을 그대로 이어받아 삭제 또는 삽입이 간단함
- 하지만 단점도 그대로 물려받아 작은 데이터들을 저장할 때 연결 리스트 자체의 오버헤드가 부담이 됨
- 버킷을 계속해서 사용하는 Open Address 방식에 비해 테이블의 확장을 늦출 수 있음

`Tree를 사용하는 방식 (Red-Black Tree)`

- 기본적인 알고리즘은 Separate Chaining 방식과 동일하며 연결 리스트 대신 트리를 사용하는 방식
- 연결 리스트를 사용할 것인가와 트리를 사용할 것인가에 대한 기준은 하나의 해시 버킷에 할당된 key-value 쌍의 개수
- 기본적으로 메모리 사용량이 많음
- 데이터 개수가 적을 때 Worst Case를 살펴보면 트리와 연결 리스트의 성능 상 차이가 거의 없음

`Open Address` vs `Separate Chaining`

일단 두 방식 모두 Worst Case 에서 O(M)이다. 하지만 Open Address방식은 연속된 공간에 데이터를 저장하기 때문에 Separate Chaining에 비해 캐시 효율이 높다. 따라서 데이터의 개수가 충분히 적다면 Open Address방식이 Separate Chaining보다 더 성능이 좋다. 한 가지 차이점이 더 존재한다. Separate Chaining방식에 비해 Open Address방식은 버킷을 계속해서 사용한다. 따라서 Separate Chaining 방식은 테이블의 확장을 보다 늦출 수 있다.

![img](https://velog.velcdn.com/post-images%2Fcyranocoding%2F329e7e60-b226-11e9-a4ce-730fc6b3757a%2F16eBeaqTti8MxWPsw4xBgw.png)

출처
https://github.com/JaeYeopHan/Interview_Question_for_Beginner/tree/master/DataStructure#hash-table
https://github.com/gyoogle/tech-interview-for-developer/blob/master/Computer%20Science/Data%20Structure/Hash.md
https://github.com/junh0328/prepare_frontend_interview/blob/main/data_structure.md#%ED%95%B4%EC%89%AC-%ED%85%8C%EC%9D%B4%EB%B8%94
https://ratsgo.github.io/data%20structure&algorithm/2017/10/25/hash/
https://velog.io/@cyranocoding/Hash-Hashing-Hash-Table%ED%95%B4%EC%8B%9C-%ED%95%B4%EC%8B%B1-%ED%95%B4%EC%8B%9C%ED%85%8C%EC%9D%B4%EB%B8%94-%EC%9E%90%EB%A3%8C%EA%B5%AC%EC%A1%B0%EC%9D%98-%EC%9D%B4%ED%95%B4-6ijyonph6o
https://velog.io/@edie_ko/hashtable-with-js#%ED%95%B4%EC%8B%9C-%EC%B6%A9%EB%8F%8C
