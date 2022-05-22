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

<br>
**02.실행 컨텍스트**
<br>
실행 컨텍스트는 실행할 코드에 제공 환경 정보들을 모아놓은 객체로 js의 동적 언어로서의 성격을 가장 잘 파악할 수 있는 개념임
자바스크립트는 어떤 실행 컨텍스트가 활성화되는 시점에, 선언된 변수를 호이스팅하고, 외부 환경 정보를 구성하고, this값을 설정 하는 등
다양한 동작을 수행하는데,
이로 인해 특이한 현상들이 팡팡팡 등장

2.1 실행 컨텍스트란?

stack - 선입 후출

queue - 선입 선출

흔히 실행 컨텍스트를 구성하는 방법은 함수를 실행하는 것 뿐이다(저역공간과 eval도 있지만 우선 제외)

함수가 실행되면 아래로 진행하는 것을 중단하고 해당 함수부분으로 이동해서 코드를 진행시킴.
js에서는 어떤 실행 컨텍스트가 활성화 될 때 자바스크립트 엔진은 해당 컨텍스트에 관련된 코드들을 실행하는데 필요한 환경 정보들을 수집해서 실행 컨텍스트 객체에 저장함.

아래와 같은 정보들이 담김
- VariableEnvironment : 현재 컨텍스트 내의 식별자들에 대한 정보와 외부 환경 정보, 선언 시점의 스냅샷-> 즉 변화 없음
- LexicalEnvironment : 처음에는 Variable과 같지만 변경사항이 실시간 반영
- ThisBinding : this 식별자가 바라봐야 할 대상 객체


2.2 Variable Environment
처음에 이것을 만들고 Lexical에 이 복사본을 사실상 넣는것임

2.3 Lexical Environment
한국어 번역으로는 어휘적 환경, 정적 환경이라고 다양하게 말하는데 그냥 언어자체로 받아들이는게 좋음

2.3.1 environmentRecord와 호이스팅
environmentRecord에는 현재 컨텍스트와 관련된 코드의 식별자 정보들이 저장됨.
전체 텍스트를 구성하는 함수에 지정된 매개변수 식별자, 함수 자체, var로 선언된 변수의 식별자 등이 식별자에 해당.

컨텍스트 내부 전체를 처음부터 끝까지 쭉 훑어나가며 순서대로 수집함.

변수정보를 수집하는 과정이 끝났더라도, 실행 컨텍스트가 관여할 코드들은 전부 실행 전의 상태임.
하지만 엔진은 호이스팅을 진행함.

[호이스팅 규칙]

environmentRecord에는 다양한 것들이 담긴다.

호이스팅은 선언을 위로 끌어올린다고 하는데, 실제로 위로 끌어올려서 실행하는것은 아니다.

-arguments
컨텍스트 생성 시점에 함께 만들어 지는 정보중 하나.
지정한 매개변수의 개수와 무관하게 호출 시 전달한 인자가 모두 arguments에 담김.
이러한 특성으로 ㅎ마수의 자율성이 높아져서 잘 사용했음.
하지만 이것은 배열이 아닌 유사 배열 객체라 활용하는데 처리가 필요함.
또한 함수 내부에서 매개변수의 값을 바꾸면 arguments 또한 바뀌게 되어,
전달된 인자를 모두 저장하는 데이터 라는 본 개념이 상실하게됨

그래서 ES6에서는 rest parameter라는 개념이 등장함.
이는 arguments 완전 대체함

아무튼 인자들과 함께 함수를 호출하는 경우 arguments에 전달된 인자를 담는것을 제외하면, 코드 내부에서 변수를 선언한 것과 다른 점이 없음.
특히나 lexicalEnvironment 입장에서 동일함.

호이스팅할때는 변수명만 끌어 올리고, 어떤 값이할당된 것인지는 그 자리에 그대로 둠
하지만 함수는 선어부 전체를 올리게 됨

[함수 선언문과 함수 표현식]

함수를 선언하는데는 선언문과 표현식의 방법이 있음.

function a () {} - 함수 선언문
a();

var b = function () {} 익명 함수 표현식 변수명 b가 곧 함수명
b();

var c = function d () {} 기명 함수 표현식 - 변수명이 c 함수명은 d
c();
d();-> error

함수명은 오직 함수 내부에서만 접근할 수 있음.
함수 내부에서는 c()로 호출하는 d()로 호출하든 산관없는데 굳이? 라는 물음이 따라옴


-함수 선언문과 함수 표현식의 실직적 차이
함수를 표현식으로 할당하게 되면 호이스팅이 변수 부분만 먼저 할당되고 이후에,
함수가 정의된 곳에가서야 함수가 정의된다.
그래서 만약 전역공간에서 이 함수가 정의되는게 중복되거나 여럿 존재하는식으로 정의되어있다면 큰일이 난다.

2.3.2 스코프, 스코프 체인, outerEnvironmentReference

스코프란 식별자에 대한 유효 범위다.
외부에서 선언한 변수는 내부에서도 접근이 가능하지만, 내부에서 선언한 변수는 오직 내부에서만 접근이 가능하다.
ES5 까지는 오직 함수에 의해서만 스코프가 생성되었다.
식별자의 유효 범위를 안에서부터 바깥으로 차례로 검색해나가는 것을 스코프체인이라고 하고,
이것을 가능하게 하는것이 LexicalEnvironment의 두번째 수집 자료인 outerEnvironmentReference다

-스코프체인
outerEnvironmentReference는 현재 호출된 함수가 선언될 당시의 LexicalEnvironment를 참조한다.
과거 시점인 선언될 당시!
선언하다라는게 실제로 일어나는 것은 콜 스택 상에서 실행 컨텍스트가 활성화 된 상태일 뿐이다.
어떤 함수를 선언하는것으로는 의미가 없으며, 그 코드가 활성화 되어야지 진짜 실행되는 것이다.

outerEnvironmentReference는 연결리스트의 형태를 띈다
선언 시점의 LexicalEnvironment를 계속 찾아 올라가면서 마지막에 전역 컨텍스트의 Lexical Environment를 찾는다.
또한 각 outerEnvironmentReference는 오직 자신이 선언된 시점의 Lexical만 참조하고 있으므로, 가장 가까운 요소로 부터 차례로 접근할 수 있고
다른 순서로 접근하는것은 아노딘다.

이렇기 때문에 여러 스코프에서 동일한 식별자를 선언했을땐, 무조건 스코프 체인 상에서 가장 먼저 발견된 식별자에만 접근이 가능해진다.

전역 컨텍스트에서 내부 컨텍스트로 들어갈 수록 규모가 작아지는 반면, 스코프 체인을 타고 접근 가능한 변수의 수는 늘어난다.
전역 공간에서는 전역 스코프에서 생성된 녀석들만,
내부에서는 전역과 내부에서 만들어진 변수들에 모두 접근이 가능한것이다.

하지만 스코프 체인 상 있는 변수라고 해서 무조건 접근이 가능한 것은 아니다.
만약 내부에서 어딘가 접근하려고 하면 스코프 체인의 첫번째 인자에서의 Lexical부터 검색해야하고,
그안에 식별자가 있기때문에 즉시 선언부만된 undefined를 반환하는 것이다.

즉 컨텍스트 내부에서 변수를 선언했기때문에, 전역공간에서 선언한 동일한 이름의 변수에는 접근을 할 수 없는 것이다.
이를 변수 은닉화 variable shadowing이라고 함.

-전역변수와 지역변수
걍 전역변수 사용 지양해야하는게 메인임

2.4 this
실행 컨텍스트의 thisbinding에는 this로 지정된 객체가 저장됨.
실행 컨텍스트 활성화 당시 this가 지정되지 않은 경우 전역 객체가 저장되고,
그밖에는 함수를 호출하는 방법에 따라 this가 나타내는 바가 달라짐.

2.5 정리
실행 컨텍스트 - 실행할 코드에 제공할 환경 정보를 모아놓은 객체.
전역 컨텍스트, eval, 함수 실행에 의한 컨텍스트 등이 있음.

실행 컨텍스트 객체는 활성화되는 시점에 variableEnvironment, LexicalEnvironment, ThisBinding 의 세 가지 정보를 수집함.

컨텍스 생성 시 Variable = Lexical
Lexical은 함수가 실행되며 바뀌는 반면 Variable은 초기 상태를 유지함.

Variable 과 Lexical은 매개 변수 명, 변수의 식별자, 선언한 함수의 함수명 등을 수집하는 environmentRecord와 바로 직전 컨텍스트의 Lexical 정보를 참조하는
outerEnvironmentReference로 구성되어 있음.

호이스팅 개념도 알아야함. -> 여기서 함수 선언문과 함수 표현식의 차이가 발생함.
environmentRecord의 수집과정을 추상화 한 개념임-> 그래서 끌어올려서 선언하는것 처럼 보이는것임.

스코프 - 변수의 유효범위
outerEnvironmentReference는 해당 함수가 선언된 위치의 lexical을 참조함.
뭔가 접근하려고 하면 현재 lexical보고 없으면 위로보고 쭉쭉 오라감.
전역 컨텍스트까지 찾아봤는데 없데용? 바로 언디파인드 리턴

전역 컨텍스트의 lexcial 담긴 변수를 전역 변수라고 하고, 그밖의 함수안에 들어간 녀석들은 다 지역변수임

this는 실행 컨텍스트를 활성화 하는 당시에 지정된 this가 저장됨.
함수를 호출하는 방법에 따라 그 값이 다라지는데, 지정하지 않으면 보통 전역 객체가 저장됨.

 <br>
**03.this**
<br>

자바스크립트에서 가장 혼란스러운 개념.
대부분의 객체지향 언어에서 This는 클래스로 생성한 인스턴스 객체를 의미.
하지만 자바스크립트에서는 어디든 this가 사용가능함.
그래서 매번 this가 달라지기 때문에 이 개념을 잘 알아두어야함.

3.1 상황에 따라 달라지는 This

자바스크립트에서 this는 기본적으로 실행 컨텍스트가 생성될 때 함께 결정.
실행 컨텍스트는 함수를 호출할 때 생성되므로, 바꿔말해 this는 함수를 호출할때 결정됨.

3.1.1 전역 공간에서의 this
전역 공간에서 this는 전역 객체를 가리킴
개념으로 따졌을때 컨텍스트를 생성하는 주체가 바로 전역객체이기 때문.
런타임 환경에 따라 다른 이름을 가지며 브라우저는 window, Nodejs에서는 global임

-전역공간의 특질
전역변수 선언 시 자바스크립트 엔진은 이를 전역객체의 프로퍼티로도 할당함.
변수이면서 객체의 프로퍼티인것임.

var a = 1;
console.log(a); // 1
console.log(window.a); // 1
console.log(this.a); // 1

위와 같은 결과가 나오는 이유는, 사실 자바스크립트의 모든 변수는 특정 객체의 프로퍼티로 작동하기 때문임.
특정 객체란 실행 컨텍스트의 LE 이며, 실행 컨텍스트는 변수를 수집해 LE의 프로퍼팆로 저장함.
이후 어떤 변수를 호출하면 LE를 조회해서 일치하는 프로퍼티가 있다면, 그 값을 반환함.
전역 컨텍스트의 경우 LE는 전역객체 그대로 참조.

윗말 조금더 정확히 하면,
'전역 변수를 선언하면 자바스크립트 엔진은 이를 전역객체의 프로퍼티로 할당함'

delete 연산자를 사용할 경우 약간 특이한 현상이 있음.
처음부터 전역 객체의 프로퍼티로 할당한 경우 delete가 적용되지만,
처음부터 전역 변수로 선언하는 경우에는 이 연산자가 작동을 하지 않음.

즉 전역 변수를 선언하면 자바스크립트 엔진이 이를 자동으로 전역 객체의 프로퍼티로 할당하면서,
추가적으로 해당 프로퍼티의 configurable속성(변경 및 삭제 가능)을 false로 정의하는 것임.

이처럼 var로 선언한 전역변수와 전역객체의 프로퍼티는 호이스팅 여부 및 configurable 여부에서 차이를 보임.

3.1.2 메서드로서 호출할 때 그 메서드 내부에서의 this

함수 vs 메서드

함수를 실행하는 두 가지 방법
1] 함수로 호출하기
2] 메서드로 호출하기

이 둘을 구분하는 유일한 차이는 독립성.

함수는 그 자체로 독립적인 기능을 수행하지만, 메서드는 자기 자신을 호출한 대상 객체에 관한 동작을 수행함.
단순히 객체 프로퍼티에 할당된 함수가 메서드가 아니라, 호출이 될 경우에만 메서드이며 그렇지 않으면 일반 함수로 실행됨.

매서드 내부에서의 this
this에는 호출한 주체에 대한 정보가 담김.
어떤 함수를 메서드로서 호출하는 경우 호출 주체는 바로 함수명 앞의 객체.
점 표기법의 경우 마지막 점 앞의 명시된 객체가 곧 this다.

3.1.3 함수로서 호출할 때 그 함수 내부에서의 this

함수 내부에서의 this
어떤 함수를 함수로서 호출할 경우에는 this가 지정되지 않음.
그런데 함수로서 호출하는 것은 호출 주체의 정보를 알 수 없음(개발자가 직접 코드로 관여한것이기 때문)
그런데 이처럼 뭔가가 지정되지 않으면 this는 전역을 바라보게 됨
=> 이건 개발자도 언급한 명백한 오류임

메서드 내부함수에서의 this
우리가 어디서 무엇을 호출하냐에 따라 이 this라는것이 시시각각 변하기 때문에
흐름을 잘 따라가면서 어떤 순서대로 코드가 실행되는지 확인해야함.
중요한것은 함수 호출한느 구문 앞에 점 또는 대괄호 표기가 있는지 없는지임.

메서드 내부 함수에서의 this를 우회하는 방법
이렇게 자꾸만 바뀌니까 this를 변수에 할당 한 후 내부함수에서 해당 값을 불러오게 되면,
지정한 this값으로 사용할 수 있음

var obj ={
outer : fuction(){

var inner1 = function(){console.log(this)}

}

inner1(); // window


var self = this;

var inner2 = function(){console.log(self)}

}

inner2(); // outer : f

}


this를 바인딩 하지 않는 함수

화살표 함수를 사용하면 this를 바인딩 하지 않아 여기저기의 값을 사용할 수 있음.

var obj ={
outer : fuction(){

var inner1 = () => {console.log(this)}

}

inner1(); // outer : f
}

call, apply를 활용해서도 명시적으로 this를 지정할 수 도 있당

3.1.4 콜백 함수 호출 시 그 함수 내부에서의 this

함수 A의 제어권을 다른 함수(또는 메서드) B에게 넘겨주는 경우 함수 A를 콜백 함수라고 함.
함수 A는 함수 B의 내부 로직에 따라 실행되며,
this또한 B 내부로직에서 정한 규칙에 따라 값이 결정됨.

콜백 함수도 함수이기 때문에 기본적으로 3.1.3절에서와 마찬가지로 this가 전역 객체를 참조하지만,
제어권을 받은 함수에서 콜백 함수에 별도로 this가 될 대상을 지정한 경우 그 대상을 참조함.

예를들어 addeventlistener 메서드 경우 콜백 함수를 호출할 때 자신의 this를 상속하도록 정의되어 있음.
즉 메서드 명의 점(.) 앞부분이 곧 this가 됨.
하지만 이또한, 무조건이라고 할 수 없는게, 콜백함수의 제어권을 가지는 함수가 this를 무엇으로 결정하는지에 따라 정해지기 때문에
항상 this가 뭘 보고 있는지 집중해야한다.

3.1.5 생성자 함수 내부에서의 this
생성자 함수는 어떤 공통된 성질을 지니는 객체들을 생성하는 데 사용하는 함수임.

객체 지향에서는 이에 생성자를 class, 클래스를 통해 만든 객체를 instance라고 일컫음.

생성자는 구체적인 인스턴스를 만들기 위한일종의 틀임.
여기에 공통적인 속성들이 준비되어있고, 구체적인 인스턴스의 개성을 더해 개별 인스턴스를 만들 수 있는 것임.

이때 this.x 로 인자들을 넣게 되는데 이 this가 가리키는 것은 생성자 함수 내부의 인스턴스를 의미함.

3.2 명시적으로 this를 바인딩 하는 법

3.2.1 call 매서드
Function.prototype.call(thisArg[, arg1[ arg2[, …]]])
call 매서드는 호출 주제인 함수를 즉시 실행하도록 하는 명령어
call 매서드의 첫번째 인자로 this를 바인딩하고 이후 인자들을 호출할 함수의 매개변수로 정함.
함수 그냥 실행하면 this는 전역객체 참조하지만, 이런 경우에는 바인딩한 임이의 객체를 this로 정하는 것임.

3.2.2 apply 메서드
Function.prototype.apply(thisArg[, argsArray]);

apply랑 call 메서드는 기능적으로 동일한데,
call 메서드는 첫 번째 인자를 제외한 나머지 모든 인자들을 호출할 함수의 매개변수로 지정하는 반면,
apply 메서드는 두 번째 인자를 배열로 받아 그 배열의 요소들을 호출할 함수의 매개변수로 지정한다는 점에서 차이가 있음.

3.2.3 call / apply 메서드의 활용
- 유사배열객체 array-like object에 배열 메서드를 적용

객체에는 배열 메서드를 직접 적용할 수 없음.
하지만 키가 0 또는 양의 정수인 프로퍼티가 존재하고, length 프로퍼티 값이 0 또는 양의 정수인 객체,
즉 배열의 구조와 유사한 객체의 경우(유사배열객체) call 또는 apply 매서드를 활용해서 배열 메서드를 차용할 수 있음.

함수 내부에서 접근할 수 있는 arguments 객체도 유사배열객체이므로 같은 방법으로 사용할 수 있음.
querySelectorAll, getElementsByClassName 으로 선택한 nodelist도 마찬가지.

ex)
var obj = {
0:'a',
1:'b',
2:'c',
length:3
};
Array.prototype.push.call(obj, 'd');

var argv = Array.prototype.slice.call(arguments);
argv.forEach(function (arg){
console.log(arg)});

단 문자열의 경우 length 프로퍼티가 읽기 전용이라, 원본 문자열에 변경을 가하는 메서드는 에어를 던지고,
concat 처럼 대상이 반드시 배열이여야 하는 경우에 에러는 나지 않지만 제대로된 결과값이 나오지 않음.

ES6 에서는 유사배열객체 또는 순회 가능한 모든 종류의 데이터 타입을 배열로 전환하는 Array.from 메소드를 새로 도입함.
=> 배열 형태로 각각 튀어나옴

- 생성자 내부에서 다른 생성자를 호출
생성자 내부에 다른 생성자와 공통된 내용이 있을 경우 call or apply를 이용해 다른 생성자를 호출하면 간단하게 반복을 줄일 수 있음
생성자 함수 내부에서 생성자 함수를 호출해 인스턴스의 속성을 정의

- 여러 인수를 묶어 하나의 배열로 전달하고 싶을 때 - apply 활용
여러개의 인수를 받는 메서드에게 하나의 배열로 인수들을 전달하고 싶을 때는 apply메서드가 좋음.
Math.max와 Math.min에 아주 좋음.
ES6 에서는 스프ㅔ드 연산자로 활용해도 괜찮음.
결국 call apply에서는 this 활용해서 명시적으로 this바인딩 하면서 함수또는 메서드 실행할 수 있지만,
이로 인해서 this를 예측하기 어려워지는 단점이 있음.

3.2.4 bind 메서드

Function.prototype.bind(thisArg[, arg1[, arg2[, … ]]])

call과 비슷하지만 즉시 호출하지는 ㅇ낳고 넘겨받은 this 및 인수들을 바탕으로 새로운 함수를 반환하기만 하는 메서드.
다시 새로운 함수를 호출할 때 인수를 넘기면 그 인수들은 기존 bind메서드를 호출할 때 전달했던 인수들의 뒤에 이어서 등록됨.
함수에 this를 미리 적용하는 것과 부분 적용함수를 구현하는 두가지 목적을 모두 가지게 됨.

name 프로퍼티
bind메서드를 적용해서 새로 만든 함수는 독특한 성질이 생기는데,
name프로퍼티에 동사 bind의 수동태인 bound라는 접두어가 붙게됨.
어떤 함수의 원본인지 찾는거라고 생각하면 됨.

var func = function (a,b){
console.log(this, a, b)}

var bind = func.bind(1,2);

console.log(func.name) // func
console.log(bind.name) // bound func

상위 컨텍스트의 this를 내부 함수나 콜백 함수에 전달하기
이전에 self 변수를 활용한 우회법이 있었는데, 이는 call apply bind쓰면 짱 깔끔해진다.

또한 콜백 함수를 인자로 받는 함수나 메서드 중에서 기본적으로 콜백 함수 내에서의 this에 관여하는 함수 또는 메서드에 대해서도 bind 메서드를 이용하면 this값을 사용자의 입맛에 맞게 바꿀 수 있음.


3.2.5 화살표 함수의 예외사항.
이 함수는 this가 아예없기 때문에, 접근하고자 하면 스코프 체인상 가장 가까운 This에 접근하게 됨.

3.2.6 별도의 인자로 this를 받는 경우(콜백 함수 내에서의 this)
콜백 함수를 인자로 받는 메서드 중 일부는 추가로 this로 지정할 객체(thisArg)를 인자로 지정할 수 있는 경우가 있음.
이런 메서드의 thisArg 값을 지정하면 콜백 함수 내부에서 this값을 원하는 대로 변경 가능.
이런 형태는 여러 내부 요소에 대해 같은 동작을 반복 수행해야하는 배열 메서드에 많이 포진돼 있으며,
Set, Map 등의 일부 메서드에도 존재.

콜백 함수와 함께 thisArg를 인자로 받는 메서드
forEach
map
filter
some
every
find
findIndex
flatMap
from
Set.prototype.forEach
Map.prototype.forEach

3.3 정리

-전역 공간에서 this는 전역객체를 참조
-어떤 함수를 메서드로 호출한 경우, this는 메서드 호출 주체(메서드 명 앞의 객체)를 참조
-어떤 함수를 함수로서 호출한 경우 this는 전역객체 참조, 메서드 내부 함수에서도 동일
-콜백 함수 내부에서의 this는 해당 콜백함수의 제어권을 넘겨받은 함수가 가지며, 정의가 없을경우 전역객체
-생성자 함수에서의 this는 생성될 인스턴스 참조

명시적 this바인딩
-call,apply = 명시적으로 this지정하고 함수 또는 메서드 호출
-bind = this 및 함수에 넘길 인수를 일부 지정해서 새로운 함수 제작
-요소를 순회하면서 콜백함수를 반복호출하는 경우의 일부 메서드는 별도의 this를 인자로 받기도 함.



 <br>
**04.콜백함수**
<br>


4.1 콜백 함수란?
콜백함수는 다른 코드의 인자로 넘겨주는 함수.
콜백 함수를 넘겨받은 코드는, 이 콜백 함수를 필요에 따라 적절한 시점에 실행

callback = 부르다, 호출하다 call + 뒤돌아오다, 되돌다 back
되돌아 호출해줘! 라는 말
어떤 함수를 호출하면서 특정 조건일때 a함수 실행해서 알려줘!
라는 요청을 보내면
그 함수가 판단하고 a 스스로 호출하는 것임.
제어권도 위임함.

4.2 제어권

4.2.1 호출 시점
scope.setInterval(func, delay[, param1, param2, …]);

scope에는 window객체 혹은 worker의 인스턴스가 들어오는데, 일반적인 브라우저 환경에서는 window생략해서 사용함.
매개변수로 func, delay받는데 필수며 delay는 ms단위
나머지 파라미터는 func 실행할때 매개변수로 전달할 인자.
func에 넘겨준 함수는 매 delay마다 실행되며, 결과로 어떠한 값도 리턴하지 않음
setInterval 실행하면 내용 자체를 특정할 수 있는 고유 id값이 반환되는데,
이를 변수에 담은 이유는 반복 실행되는 중간에 종료할수있게끔임.
clearInterval

4.2.2 인자

Array.prototype.map(vallback[, thisArg])
callback : function(CurrentValue, index, array)

map 매서드는 메서드의 대상이 되는 배열의 모든 요소들을 처음부터 끝까지 하나씩 꺼내어
콜백 함수를 반복 호출하고,
콜백함수의 실행 결과들을 모아 새로운 배열을 만듦.
(CurrentValue, index, array)
현재 배열, 인덱스, 결과 배열

이렇듯 콜백함수 제어권 넘길땐, 함수 메서드에 맞는 인자들을 제대로 넘기고 확인해야함.

4.2.3 this
콜백함수도 함수이기때문에 기본적으로 this가 전역객체 참조하지만, 만약 bind한 경우 그것을 따름.

map함수를 자세히 보면 아래와 비슷
Array.prototype.map = function (callback, thisArg){
var amppedArr = [];
for (var i = 0; i< this.length; i++){


^var mappedValue = callback.call(thisArg || window, this[i], i, this);^


mappedArr[i] = mappedValue;
}
return mappedArr;
};

this에는 ThisArg값이 있을 경우 그 값을,
없을 경우 전역 객체를 지정하고
인자1 - 배열의 i 요소
인자2 - i
인자3 - 배열 자체 지정
하여 호출함.

4.3 콜백 함수는 함수다.
콜백 함수로 어떤 객체의 메서드를 전달하더라도, 그 메서드는 메서드가 아닌 함수로써 호출됨.
함수만 가리키게 되면 이전에 말했던것처럼, this가 전역 객체를 바라보게 됨.

결국 뭔가를 부르고 호출하지 않으면 함수는 그 함수자체로 함수라는 말이다.

4.4 콜백 함수 내부의 this에 다른 값 바인딩하기
객체의 메서드를 콜백 함수로 전달하면 해당 객체를 this로 바라볼 수 없게 된다.
콜백 함수 내부에서 this가 객체를 바라보게 하고 싶다면?
별도의 인자로 만들어 넘겨줘도 되지만, 그렇지 않은 경우, this의 제어권도 넘겨주게 되서 사용자가 임의로 변경 불가능.
그래서 전통적으로는 this를 다른 변수에 담아 콜백 함수로 활용할 함수에서는 this대신 그 변수를 사용하게 하고,
이를 클로저로 만드는 방식이 많이 사용됨.

1.함수 내부의 this에 다른 값 바인딩 - 전통적
var obj1 = {
name : 'obj1',
func : function () {
var self = this;
return function() {
console.log(self.name)
}
}

var callback = obj1.func();
setTimeout(callback, 1000)

2.콜백 함수 내부에서 this를 사용하지 않는 경우
var obj1 = {
name :'obj1',
func:function (){
console.log(obj1.name)
}
}
setTimeout(obj1.func, 1000);

3.func함수 재활용

var obj2 = {
name:'obj2',
func:obj1.func
}

var callback2= obj2.func();
setTime(callback2,1500);

var obj3 = {name:'obj3'};
var callback3 = obj1.func.call(obj3);
setTimeout(callback3, 2000);

4.ES5 bind method
var obj1 = {

name:'obj1',
func:function () {
console.log(this.name)
}
};

setTimeout(obj1.func.bind(obj1), 1000);

var obj2 = {name:'obj2'};
setTimeout(obj1.func.bind(obj2),1500);

4.5 콜백 지옥과 비동기 제어
콜백 지옥은 콜백 함수를 익명 함수로 전달하는 과정이 반복되어 코드의 들여쓰기 수준이 더러워지는 현상이다.
js에서 흔히 발생하는 문제인데, 주로 이벤트 처리나 서버 통신과 같이 비동기적인 작업을 수행하기 위해 이러한 형태가 자주 등장하는데,
가독성도 떨어지고 코드 수정도 어려움

비동기 <===> 동기
동기적인 코드는 현재 실행 중인 코드가 완료된 후에 다음 코드를 실행하는 방식.
반대로 비동기적인 코드는 현재 실행 중인 코드의 완료 여부와 무관하게 즉시 다음 코드로 넘어감.
CPU의 계산에 의해 즉시 처리가 가능한 대부분의 코드는 동기적임.
계산식이 복잡해서 CPU가 계산하는데 시간이 많이 필요한 경우라고 해도 이는 동기적인 코드임.
반면 사용자의 요청에 의해 특정 시간이 경과되기전 함수의 실행을 보류하거나,
사용자 개입이 있을때 실행하도록 대기하거나,
웹브라우저 자체가 아닌 다른 대상에 요청하고 그 응답이 왔을때 함수를 실행하도록 대기하는 등,
별도의 요청, 실행 대기, 보류 등과 관련된 코드는 비동기적인 코드임.

현대 js는 웹 복잡도 높아지면서 비동기 코드 많아지고 그로인해 콜백지옥이 커지고 있음.

콜백함수 계속해서 쓰게되면 전달되는 순서가 아래 => 위 로 향해서 어색하게 느껴짐
해결하는 방법중 하나는 모두 기명함수로 변경하는것이 있는데,
이는 귀찮고 헷갈릴수도 있음.

그래서 ES6에서 promise,generator가 도입되고 es2017에서는 async,await가 도입됨.

new Promise(function (resolve){
setTimeout(function () {
var name = '에스프레소';
console.log(name);
resolve(name);
}, 500)
}).then(function(prevName){
return new Promise(function(resolve){
….

이런식으로 진행됨.

new 연산자와 함께 호출한 promise의 인자로 넘겨주는 콜백함수는 호출할때 바로 실행됨.
내부에 resolve또는 reject가 있으면, 둘 중 하나가 실행되기 전까지 다음 then 또는 오류 구문(catch)로 넘어가지 않음.
비동기가 완료되어야만 resolve, reject가 되니 비동기 작업의 동기적 표현이 가능해짐.

-Generator
var addCoffee = function(prevName, name){
setTimeout(function(){
coffeeMaker.next(prevName ? prevName + ','+name : name);
}, 500);
};

var coffeeGenerator = function* () {
var espresso = yield addCoffee('', '에스프레소');
console.log(espresso);
var americano = yield addCoffee(espresso, '아메리카노');
…..

};
var coffeeMaket = coffeeGenerator();
coffeeMaker.next();

*붙은게 generator임.
generator함수 실행하면 iterator가 반환되는데, iterator는 next라는 메소드를 가짐
next 호출하면 generator함수 내부에서 가장 먼저 등장하는 yield에서 함수의 실행을 멈춤.
이후 다시 next 메서드 호출하면, 앞서 멈췄던 부분부터 시작해서 그다음 yield에서 멈춤.
즉 비동기 작업이 완료되는 시점마다 next호출해주면 generator가 위에서 아래로 순서대로 진행되는 것임.

그런데 위에 내용이 어려워서 아래처럼 async/await이 가독성도 좋고 좋은 것 같다.

var addCoffee = function (name) {
return new Promise(function (resolve){
	setTimeout(function(){
resolve(name);
},500)})}

var coffeeMaker = async function () {
var coffeeList = '';
var _addCoffee = async function(name){
coffeeList += (coffeeList ? ',' : '') + await addCoffee(name)}

await _addCoffee('에스프레소);
console.log(coffeeList)
await _addCoffee('아메리카노');
console.log(coffeeList)
….
}
coffeeMaker();


4.6 정리
콜백 함수는 다른 코드에 인자로 넘겨줌으로써 그 제어권도 함께 넘김
제어권 넘겨받은 코드는 
1. 콜백함수 호출 하는 시점 스스로 판단해서 실행
2. 콜백 함수 호출 시, 넘겨줄 값들 및 순서가 정해져있고, 순서따르지 않고 코딩하면 띠로롱 하고 나옴
3. 콜백함수 this가 뭘 볼지 정해져 있는 경우도 있어서, 만약 원하지 않는다면 bind 사용하기
4. 함수에 인자로 메서드 전달해도 결국 함수로 실행됨
5. 비동기 제어 위해 콜백 함수 사용하다보면 콜백지옥 빠지니, Promise,Generator,async/await 사용해보기


 <br>
**05.클로저**
<br>

5.1 클로저의 의미 및 원리 이해
클로저는 여러 함수형 프로그래밍 언어에 등장하는 보편적 특성임.
MDN - 클로저는 함수와 그 함수가 선언될 당시의 le의 상호관계에 따른 현상
내부함수에서 외부 변수를 참조하는 경우에 해당

즉, 어떤 ㅎ마수에서 선언한 변수를 참조하는 내부함수에서만 발생하는 현상.

var outer = function () {
var a =1;
var inner = function () {
console.log(++a);
};
inner();
};
outer();

위 함수의 흐름
1.[]

2.[전역 컨텍스트]

3.Outer[LE - environmentRecord : {a:1, inner:f} -outerEnvironmentReference : {outer :1}]
[전역 컨텍스트]

4.Inner[LE - environmentRecord : {a:1=>2, inner:f} -outerEnvironmentReference : {outer :1}]
Outer[LE - environmentRecord : {a:1=>2, inner:f} -outerEnvironmentReference : {outer :1}]
[전역 컨텍스트]

5.Outer[LE - environmentRecord : {a:1=>2, inner:f} -outerEnvironmentReference : {outer :1}]
[전역 컨텍스트]

6.[전역 컨텍스트]

7.[]

하지만 위와 같은 방식은 내부 함수를 재사용 하는것이 불가능

var outer = function () {
var a =1;
var inner = function () {
return ++a;
};
return inner;
};
var outer2 = outer();
console.log(outer2());
console.log(outer2());

위 함수의 흐름

1.[]

2.전역 environmentRecord : { outer : f, outer2:undefined}

3.outer - environmentRecord : {a :1, inner : f} - outerEnvironmentRecord : {outer :f }
전역 environmentRecord : { outer : f, outer2:undefined}

4.(outer) environmentRecord : {a :1} <- 나머지 부분은 지워짐
전역 environmentRecord : { outer : f, outer2:undefined}

5.inner - environmentRecord : {} - outerEnvironmentRecord : {a:1 => 2 => 3}
(outer) environmentRecord : {a :1=> 2 => 3}  
전역 environmentRecord : { outer : f, outer2:undefined}
 
6.outer {a:3}
[전역]

7.[]

보통 함수가 끝나면 le가 gc에 들어가게 되는데, 사실 gc는 그 값이 하나도 참조가 되지 않는 경우에만 해당된다.
outer에서 inner함수를 반환하는 것 자체가, 언젠가 내부 함수가 실행될 것을 암시하기 때문에 그 가능성을 열어두는 것이다.
위와 같은 것이 일단 클로저의 기본 베이스가 된다는 것이다.

다시 내용을 고치면,
클로저란 어떤 함수 a에서 선언한 변수 a를 참조하는 내부함수 b를 외부로 전달할 경우 a의 실행 컨텍스트가 종료된 이후에도 변수 a가 사라지지 않는 현상

하지만 여기서도 외부전달이 무조건 return 만을 의미하는 것은 아님
setinterval 혹은 addeventlistener처럼 handler 함수 내부에서 지역변수를 참조하도록 하는 그런것도 다 클로저로 침.

5.2 클로저와 메모리 관리
클로저는 객체 지향과 함수형 모두를 아우름.
메모리 누수 때문에 이를 지양해야한다는 사람도 있지만 이는 본질적인 특징일 뿐임.
(아무래도 컨텍스트 종료 후에도 변수가 저장된 공간이 gc로 가지 않으니 메모리 낭비라고 말하는듯)
최근 js에서는 이는 의도대로 설계한 메모리 소모의 범주에 든다.

그렇다면 혹시 이 메모리를 제거하려면 어떻게 해야할까?
참조 카운트를 0으로 만들면 gc로 들어가서 소모된 메모리가 회수될 것이다.
이를 0으로 만들기 위해서는 식별자에 참조형이 아닌 기본형 데이터(보통 null of undefined)를 할당하면 된다.

1.return 에 의한 클로저의 메모리 해제
var outer = {function () {
var a = 1;
var inner = function () {
return ++a;
};
return inner;
})();
console.log(outer());
console.log(outer());
outer = null; // null로 참조를 끊어버리는 것

2)setInterval에 의한 클로저의 메모리 해제
(function () {
var a = 0;
var intervalId = null;
var inner = function () {
if(++a >= 10){
clearInterval(intervalId);
inner = null; // 함수가 실행되고 나면 함수의 참조를 끊어버림
}
console.log(a);
};
intervalId = setInterval(inner, 1000);
})();

3)eventListener에 의한 클로저의 메모리 해제
button.removeEvnetListener('click',clickHandler);
clickHandler = null; // 이렇게 끊어버리긔

5.3 클로저 활용 사례

이해는 했는데 어따쓰냥

5.3.1 콜백 함수 내부에서 외부 데이터를 사용하고자 할 때

5.3.2 접근 권한 제어(정보 은닉)
어떤 모듈의 내부 로직에 대해 외부로의 노출을 최소화해서, 모듈간의 결합도를 낮추고 유연성을 높이고자 하는 현대 프로그래밍 언어의 중요한 개념
흔히 접근 권한에는 public, private, protected 가 있음.
return을 활용해서 선태걱으로 외부 스코프에서 함수 내부의 변수들 중 선택적으로 일부 변수에 대한 접근 권한을 부여할 수 있음.

개념적으로 전역 객체에 대해 outer함수는 참조가능하지만 그 내부에 있는 inner를 보지는 못하는 것임
그래서 내부에서 return을 통해 외부에 정보를 제공하는 유일한 방법인것임.

즉 외부에 제공하는 정보들을 모아서 return 하고, 그렇지 않은 정보는 return하지 않는것으로 접근 권한 제어가 가능한 것임.
return한 변수들은 public // 그렇지 않은 변수들은 private

만약 자동차 게임같은거 만들면 웹에서 객체 자동차를 생성하면서 이런저런 것들 할수 있음.
근데 연료량이라던지 연비라던지 마음대로 변수에 접근해서 변경해버릴 수가 있는것임.
그럴때 클로저를 활용하는 것.
즉 자동차를 객체가 아닌 함수로 만들고, 필요한 멤버만 return 하는 것

get이랑 set같은것들을 사용하면 진짜 내가 내보내기 원하는 녀석들만 내보낼수있다.

return {
get moved () {
return moved;
},
run : function(){
var km = Math.ceil(Math.random() * 6);
var wasteFuel = km / power;
if(fuel < wasteFeul) {
console.log('이동불가');
return 
} 
fuel -= wasteFuel;
moved += km;
console.log(km + 'km 이동 ( 총' + ~~~' + fuel);

var car = createCar()
이렇게 자동차 불러오고
get으로 moved만 리턴하기 때문에, fuel power같은 것에 함부로 접근하는 것이 불가능함.

하지만 여전히 run method를 덮어쓰는건 가능함.


var public Members = {}
Object.freeze(publicMembers);
return publicMembers;

이런 식으로 하면 외부에서 바꾸지 못함.

클로저 결국 쓰면 맘대로 못바꾸니까 더 안전하군요

즉 클로저를 활용해 접근권한을 제어하는 방법
1.함수에서 지역 변수 및 내부함수 등을  생성한다.
2.외부에 접근권한을 주고자 하는 대상들로 구성된 참조형 데이터(대상이 여럿일때는 객체 또는 배열, 하나일때는 함수)를 return한다.
=> return한 변수들은 공개 멤버가 되고, 그렇지 않은 변수들은 비공개 멤버가 됨.

5.3.3 부분 적용 함수
n개의 인자를 받는 함수에 미리 m개의 인자만 넘겨 기억시켰다가, 나중에 (n-m)개의 인자를 넘기면
비로소 원래 함수의 결과를 얻을 수 있게끔 하는 함수.
즉 this binding인것ㅇ미


var add = function () {더해서 리턴하는 식}

var addPartial = add.bind(null,1,2,3,4,5);
addPartial(6,7,8,9,10) => 55

근데 위에는 this의 값을 변경할 수 밖에 없기 때문에 메서드에서 사용은 힘듦

var partial = function () { // add 1 2 3 4 5
var orgArgs = arguments; // add 1 2 3 4 5
var func = orgArgs[0]; // 왜냐 밑에 addpartial을 정의하는 부분에서 add함수를 첨음에 추가해줬기 때문임.
if( 함수라면 throw new Error)
return () {
var partialArgs = Array.prototype.slice.call(originalParialArgs,1)  // 1 2 3 4 5 
var restArgs = Array.prototype.slice.call(arguments); // add 1 2 3 4 5
return func.apply(this, partialArgs.concat(resstArgs)); // 나머지 인자들을 받아 이들을 한데 모아 원본 함수를 호출 ???
}

var add = function () {
대충 아규먼츠 들어오면 더하는 내용}

var addPartial = partial(add,1,2,3,4,5);
addPartial(6,7,8,9,10) // 55

원하는 자리에 인자 넣기

Object.defineProperty(window, '-', {
value : 'EMPTY_SPACE',
writable:false,
configurable:false,
enumerable:false,})

var partial2 = function () {
var originalPartialArgs = arguments;
var func = origi~~[0]
함수아니면 에러던지기

return function (){
var partialArgs = Array.prototype.slice.call(originalParialArgs,1) 
var restArgs = Array.prototype.slice.call(arguments);
for(var i =0l i< partialArgs.length; i++){
if(partialArgs[i] === _) {
partialArgs[i] = restArgs.shift()//앞에서부터 인자 빼서 전달}}

return func.apply(this, partialArgs.concat(restArgs))

return func.apply(this, partialArgs.concat(resstArgs));


var addPartial = partial(add,1,2,_,4,_); // 빈곳에 맞춰서 수가 들어감
addPartial(3,5) 

디바운스 함수로 구현
기타내용 복습 -> 기록x
