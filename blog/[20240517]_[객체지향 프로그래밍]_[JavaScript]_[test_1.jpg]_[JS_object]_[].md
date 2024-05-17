
# 객체지향 프로그래밍

[객체지향 프로그래밍](https://www.notion.so/22624154c79941358b72da55f94fe923?pvs=21) 

- 설명
    
    객체지향 프로그래밍은 모든걸 객체화 해서 프로그래밍 한다는 것!
    
    <aside>
    🛠 게임을 만드는데
    
    늑대라는 몬스터를 만들때
    
    늑대는 프로그램화 해야하는 대상
    
    늑대가 객체가 되는거임
    
    늑대가 공격을 하고 늑대의 행위 이런것들은 메서드
    그냥 늑대가 가진 레벨, 등의 속성들은 값
    
    </aside>
    
    객체화 한다 = 추상화 한다.
    
    모든 부분을 다 표현할 수 없지만 특징들을 표현하는 것.
    
    객체지향 프로그래밍 - 프로그래밍의 방법론
    
    꼭 지켜야하는게 아니라, 꼭 객체를 만들어야 할 필요는 없지만 이런 방법이 있다. 라는 느낌 
    

- 실습 : 여러분 자신을 추상화 해봅시다. 그리고 상호작용 하고 싶은 대상을 만들어보고 서로 상호 작용 할 수 있는 메소드를 만들어 봅시다.

```jsx
const me = {
	name: "이상윤",
	age: 5,
	thumbsUp : function(person){
				person.emotion();
	}
}
```

```jsx
const ormi1 = {
		comment: "감사합니다",
		emotion: function(){
				this.comment += "👍"
		}
}

const ormi2 = {
		comment: "안녕하세요",
		emotion: function(){
				this.comment += "👍"
		}
}
```

![image](img/240517_img0.png)

## 생성자

- 설명
    
    객체를 만드는 함수
    
    객체를 어떻게든 만들 수있는데 왜 굳이 생성자를 사용해야하나?
    
    - 같은 프로퍼티와 메서드를 공유할 수 있다.
    
    인스턴스 - 객체는 객체인데 생성자 함수로 만들어진 객체
    
    **생성자 함수와 객체의 관계는 instanceof 로 확인**
    
    ```jsx
    robot1 instanceof Factory
    ```
    

같은 기능과 같은 키를 가지는 개체를 여러개 만들때

```jsx
{
	name: "robot1",
	sayYourName: function(){
		console.log("robot1"입니다);
}

{
	name: "robot2",
	sayYourName: function(){
		console.log("robot2"입니다);
}

{
	name: "robot3",
	sayYourName: function(){
		console.log("robot3"입니다);
}

{
	name: "robot14",
	sayYourName: function(){
		console.log("robot14"입니다);
}
```

위처럼 이런 객체들을 만들 때 객체를 빠르고 쉽게 많이 만들 수 있게 하는 생성자.

```jsx
function constructure(name) {
		this.name = name
		this.sayYourName = function(){
			console.log(저는 `${this.name}`입니다.}
		}
}
```

## 프로토타입

- 설명
    
    prototype은 특정 객체에 대한 참조
    
    this 처럼 어떤 공간을 가리키고 있다.
    
    인스턴스들이 공유하는 공간을 가리킴
    
    __proto__ 까지는 몰라도 된다. 
    

- 실습2: 우리가 객체지향 개념에서 만들었던 ‘나’ 와 ‘대상’ 객체를 생성자를 통해서 만들어 볼 수 있도록 코드를 수정해봅시다.

```jsx
//위에서 만든 객체

const me = {
	name: "이상윤",
	age: 5,
	thumbsUp : function(person){
				person.emotion();
	}
}

```

```jsx
const ormi1 = {
		comment: "감사합니다",
		emotion: function(){
				this.comment += "👍"
		}
}

const ormi2 = {
		comment: "안녕하세요",
		emotion: function(){
				this.comment += "👍"
		}
}
```

```jsx
// 그냥 생성자로 생성
function CreateMe () {
		this.name = "이상윤";
		this.age = 5;
		this.thumbsUp = function(person){
				person.emotion();
		}
}

// 프로토 타입 이용
function CreateOrmi (content) {
		this.content = content;
}

CreateOrmi.prototype.emotion = function(){
		this.content += "👍";
}
```

결과

![Untitled](img/240517_img1.png)

객체의 메서드를 배열에서도 쓸 수 있게 된다.

- 캡쳐사진
    
    ![Untitled](img/240517_img2.png)
    
    ![Untitled](img/240517_img3.png)
	
    
    프로토 타입 체이닝
    

## classes

[7.4 classes](https://www.notion.so/7-4-classes-e1aa2c96d4e64b47a458ece5aedd31fd?pvs=21) 

- 설명
    
    결국 객체를 만들던 생성자랑 같지만 문법적으로 시각적으로 깔끔하게 생성 가능
    
    ```jsx
    class 클래스명 {
    		constructor(){
    				// 프로퍼티 작성
    		}
    		
    		//메서드 그대로 작성
    		
    		메서드명(){
    				
    		}
    }
    ```
    
    ```jsx
    const 인스턴스명 = new 클래스명();
    ```
    

실습

```jsx
class CreateMe2 {
		constructor(){
			this.name = "이상윤";
			this.age = 5;
		}
	
		thumbsUp(person) {
			person.emotion();
		}	
}

class CreateOrmi2 {
		constructor(content) {
				this.content = content
		}
		
		emotion() {
				this.content += "👍"
		}
}
```

```jsx
const me2 = new CreateMe2(); // me2 = {name: 이상윤, age: 5}

const ormi20 = new CreateOrmi2('안녕하세요'); // ormi2 = {content: '안녕하세요'}

me2.thumbsUp(ormi20); // ormi2 = {content: '안녕하세요👍'}
```