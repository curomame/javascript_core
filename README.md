# javascript_core
<br>
**01.Data Type**
<br>
데이터를 처리하는 과정을 보면서 기본형과 참조형 타입이 다르게 동작하는 이유를 이해하고, 이를 적절히 활용 할 수 있게 되는것
1.1 데이터 타입의 종류

자바스크립트의 데이터 타입에는 크게 두 가지가 있음.
1. 기본형(원시형)
- 숫자
- 문자열
- 불리언
- null
- undefined
- Symbol(ES6)

[특성]
- 값이 담긴 주솟값을 바로 복제
- 불변성(immutability)

2. 참조형(레퍼런스)
- objcet
- array
- function
- date
- regexp(정규표현식)
- map(ES6)
- WeakMap(ES6)
- Set(ES6)
- WeakSet(ES6)

[특성]
- 값이 담긴 이루어진묶음을 가리키는 주솟값을 복제


1.2 데이터 타입에 관한 배경지식

1.2.1 메모리와 데이터

옛날에는 메모리낭비를 최소화 하기 위해 데이터 타입별로 메모리를 할당해 두었음.
지금 컴퓨터 좋고 메모리도 국밥이라 자바스크립트에서는 기본적으로 64비트 기반.
그래서 형변환을 따로 안해줘도 됨

모든 데이터는 바이트 단위의 식별자, 정확하게는 메모리 주솟값을 통해 서로를 구분짓고 연결지음

1.2.2 식별자와 변수

변수 - 변할 수 있는 수[데이터](반드시 숫자일 필요는 없음)
식별자 - 변수명

1.3 변수 선언과 데이터 할당

1.3.1 변수 선언

var a ; => 변할 수 있는 데이터를 만든다. 이 데이터의 식별자는 a로 한다.
메모리의 비어있는 공간 하나를 확보한 후 공간의 식별자를 a라고 지정하는 것.
만약 a에 접근하고자 한다면 a라는 이름을 가진 주소를 검색해 해당 공간의 데이터를 반환함

1.3.2 데이터 할당
var a;
a = 'abc';

var a ='abc';

주소에 데이터를 이름과 값으로 저장한다.
변수영역과 데이터 영역을 나누어 저장함.

주소 - 데이터 형식으로 서로가 서로를 잇고있는 모습.
데이터를 효율적으로, 자유롭게 처리하기 위해서 이러한 과정으로 데이터를 저장한다.

데이터를 수정하거나 추가할때도 이러한 방식으로 데이터 영역에 새로운 주소를 부여해 값을 부여한다.

1.4 기본형 데이터와 참조형 데이터

1.4.1 불변값
변수와 상수를 구분하는 성질은 '변경 가능성'

변경 가능성을 이야기하는 것은 - 변수 영역의 변경
불변성에 대한 이야기를 하는 것은 -데이터 영역의 변경

불변값 !== 상수
기본형 데이터는 모두 불변값이다.

1.4.2 가변값

기본형 데이터가 불변값인데 반해 참조형 데이터는 보펹거으로는 가변값을 가진다.
참조형 데이터 선언시 아래와 같은 순서로 데이터 할당이 이루어 짐

var obj1 = {
a:1,
b:'bbb'
}

1) 변수 영역에 key obj1 val 데이터 영역 주소로 할당 된후
2) 데이터 영역 부분의 해당 주소에 객체 변수영역의 주소값의 범위가 주어진다.
3) 객체 변수 영역의 데이터 부분에 객체의 key val부분이 주어지며,
4) 이 val 부분은 다시끔 데이터영역이 가진 값의 주소값을 가지게 된다.

만약 obj1.a = 2; 라고 변경을 진행하게 되는 경우에는
변수영역은 변하지 않은 채, 객체의 변수영역의 해당 key값의 val부분의 주소부분만 새로운 데이터 영역의 주소값으로 업데이트 되는 형식이다.

이렇게 단순 문자나 숫자를 넣는것 이외에도 중복으로 객체를 할당할 수도 있다.
(참고로 배열도 자바스크립에서 일종의 객체다.)

var obj = { arr:[1,2,3]};

이렇게 되는 경우에는 위의 할당 순서와 똑같이 이루어지는데 
4) 부분에서 데이터 영역이 가진 주소값을 갖게되고,
5) 해당 데이터 영역은 새로운 배열 변수 영역의 주솟값을 가져서
6) 해당 변수 영역에 key(idx) val 형식으로 데이터가 부여된다.

그렇다면 만약 이 상태에서 새로운 재할당 명령을 내리게 되면 어떨까?

arr = 'srt';

이렇게 된다면 위의 3)부분에서 arr에 부여된 val이 데이터영역에 새로 할당된 'srt'의 주솟값을 갖게되며,
5), 6)에서 만들어진 배열의 참조 값과, 데이터영역에서 배열의 주솟값은 GC(garbage collector)의 수거 대상이 된다.
이 수거 대상들은 보통 런타임 환경에 따라 메모리가 찰때마다 수거되며 빈 메모리로 바뀐다.

1.4.3 변수 복사 비교

기본형과 참조형은 불변성의 유무 때문에 변수를 복사하는데 있어 차이가 있다.

var a = 10;
var b = a;

var obj1 = {c:10, d:'ddd'};
var obj2 = obj1;

위와 같이 데이터를 정의짓고 변수를 복사한다면,

[기본형]에서는
1) 변수 a가 변수영역에 지정되고
2) 데이터 영역에 10이라는 변수가 저장된다.
3) b라는 변수 또한 변수 영역에 지정 되고,
4) b의 value 부분은 변수 a와 똑같은 주소를 바라본다.

[참조형]에서는
1) 객체 obj1이 선언되면 변수영역에 obj1할당 후 값으로 주소값을 가지며
2) 해당 주소값은 새로운 객체의 변수영역 주소값을 가지게 되고
3) 데이터 영역의 value값은 해당 변수영역의 주소값을 보게 된다.
4) 복사한 데이터는 변수영역과 데이터 영역 그리고 참조 변수영역까지 똑같은 곳을 바라보게 된다.

이후 값을 변경하면 놀래미다.

var a = 10;
var b = a;

var obj1 = {c:10, d:'ddd'};
var obj2 = obj1;

b = 15;
obj2.c = 20;

[기본형]같은 경우에는 별다른 문제없이 변수영역 b에서의 value값이 보고있던 주소를
새로 할당해서 그 공간에 15라는 수를 넣고 주소를 변경해주는 식으로 진행된다.

하지만 [참조형]에서는 객체의 변수영역에 주소값의 key가 c인 녀석을 찾아 그 value값을 데이터영역에 새롭게 20이라고 부여한 후
그 주소를 가르키게 되는 것이다.

즉 다시말하자면 obj1이 그 곳을 같이 바라보고 있으니 obj1 === obj2가 되는 셈이다.

뭔가 비유할 수 있는 것이 있다면 비유하고 싶은데,
뭐랄까…. 기본형은 사람세계에서의 이름이면 참조형은 유전자? 같은 느낌이라고 하면 나중에 내가 교육을 할때 좀 편하게 할수있으려나!

만약 제대로된 변경을 하고 싶다면 객체 자체를 부여하는것이 좋다

obj2 = {c:15, d:'asf');

이러면 obj2에 대해 새로운 객체 참조 공간이 생기고 obj2의 변수부분에서 바라보는 value가 새로이 바뀌게 되는 것이다!

1.5 불변 객체

1.5.1 불변 객체를 만드는 간단한 방법

내부 프로퍼티를 변경할 필요가 있을 때마다 매번 새로운 객체를 만들어 재할당하기로 규칙을 정하기
자동으로 새로운 객체를 만드는 도구를 활용

-> 위와 같은 방법으로 불변성을 확보할 수 있음.

방법 1> 하드코딩
방법 2> 얕은 복사(for in을 통해 새로이 객체 만들기)
방법 3> copyObject(obj);

전부 다 얕은 복사임

1.5.2 얕은 복사와 깊은 복사

얕은 복사 - 바로 아래 단계의 값만 복사
깊은 복사 - 내부의 값까지 전부 찾아서 복사

즉 얕은 복사는 객체안의 객체까지 제대로 된 복사를 진행하지 못한다.

다양한 방법들이 있는데 JSON을 문자열로 바꿨다가 다시 JSON형식으로 바꾸는 방법을 사용하는 것이 편함.

1.6 undefined 와 null

undefined가 등장하는 경우

1] 값을 대입하지 않은 변수, 즉 데이터 영역의 메모리 주소를 지정하지 않은 식별자에 접근할때
2] 객체 내부의 존재하지 않는 프로퍼티에 접근하려고 할 때
3] return 문이 없거나 호출되지 않는 함수의 실행 결과

undefined !==  empty

배열도 객체이기 때문에, 존재하지 않는 프로퍼티에 대해서 순회할 수 없음.
배열은 무조건 length 프로퍼티의 개수만큼 빈 공간을 확보하고 각 공간에 인덱스 이름을 지정할것 같지만,
실제로는 객체와 마찬가지로 특정 인덱스 값을 지정할 때 비로소 빈 공간을 확보하고 인덱스를 이름으로 지정하고 데이터 주솟값을 저장함.

즉 undefined는 그 자체로 하나의 "값" 임
=> 만약 var a; 라고 지정을 한다면 사실상 a라는 변수에 undefined이라는 값을 지정해주는거나 다름 없음

대신에 처음부터 비어있다는 것을 표현하기 위해 null을 사용할 수 있는데
null은 typeof가 object로 나오는 js 자체의 버그가 있음.
그래서 해당 값을 확인하기 위해서는 일치연산자(===)를 활용해 정확한 확인을 해야함

1.7 정리

[js data type]
기본형 - 불변값 / 참조형 - 가변값

[변수]
변경 가능한 데이터가 담길 수 있는 공간

[식별자]
그 변수의 이름

불변 객체는 최근 js에서 가장 핫한 이슈
사용자가 없음을 표현하기 위해 명시적으로 undefined을 대입하는 것은 좋지 아니함.



