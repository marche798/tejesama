# <의존성 주입 소개>
## 의존성 주입이란??
  - 의존성 주입(Dependency Injection) : 객체 조립과 설정을 위한 소프트웨어 디자인 패턴<br>
  - Angular 에서는 기본적으로 생성자 의존성 주입 패턴을 이용해 의존성을 주입 받음.<br>
```typescript
	constructor(private speedmeter: Speedmeter, public engine:Engine) {
		.....
	}
```
  - Angular 의존성 주입 시 일어나는 중간 과정을 설정하거나 타입스크립트가 지원하지 못하는 인터페이스 형을 주입받게 하는 등 여러가지 제약을 극복할 방법을 제공.

## 의존성 주입의 필요성
  - Angular는 컴포넌트 기반 개발을 하므로 컴포넌트마다 제공하는 객체 생성과 설정을 컴포넌트 내부에서 처리하는 것은 문제가 된다.<br>
  - 의존성 주입을 활용하면 객체 생성과 설정에 들어가는 코드를 최소화하고 컴포넌트마다 일관된 방법으로 생성한 객체를 제공할 수도 있다.

## 주입기 트리
  - Angular는 컴포넌트 구성에 따라 주입기 트리가 만들어진다.<br>
  - 컴포넌트마다 하나의 주입기를 갖는다.(주입기 트리는 컴포넌트 모양과 일치)<br>
![injector_tree](https://github.com/marche798/tejesama/blob/master/injector_tree.png?raw=true)

--- 

# <제공자 - 의존성 주입 시 사용할 의존성 주입 방법을 결정하는 방법 제공>
## 1. 제공자를 통한 의존성 주입
![provider_injection_process](https://github.com/marche798/tejesama/blob/master/provider_injection_process.png?raw=true)
  + 1)@injectable 장식자로 주입할 클래스 선택<br>
	해당클래스가 의존성 주입 대상임을 명시, 생략할 수 있으나 의존성 주입 대상인지 여부가 불분명해지므로 선언하자!<br>
	변수나 함수에는 사용불가
```typescript
	import { Injectable } from '@angular/core';
	...

	@Injectable()
	export class Engine {
	  ...
	}
```

  + 2)주입할 클래스를 제공자에 등록 및 3)생성자로 의존성 주입
```typescript
	import { Engine } from './engine.service';
	...

	@Component({
	 ...
	 providers: [Engine]	
	})
	export class CarComponent {
	 constructor(public engine: Engine) { ... }
	}
```

  + 제공자의 종류
    - 값 제공자 : 컨포넌트에 값을 제공 _(source : value-provider)_<br>
	```typescript
		export  let ValueProvider = 
		{
			provide : 값 제공자에 사용할 클래스 ,
			useValue : 사용할 값 변수
		};
	```
    - 팩토리 제공자 : 컴포넌트에 새로운 객체를 만들어 제공<br>
	```typescript
		export  let FactoryProvider = 
		{
			provide : 최종적으로 사용할 객체의 클래스 ,
			useFactory : 팩토리 메서드,
			deps : [의존 클래스...]
		};
	```
    - 클래스 제공자 : 클래스 제공자를 통해 클래스 간 의존 관계를 고려해 만든 객체를 컴포넌트에 제공<br>
    		 1) 대체 클래스 제공자 : 제공할 클래스를 다른 클래스로 대체하는 의존성 주입 방법을 제공
			```typescript
				providers: [주입할 클래스..]
			```
		 2) 가명 클래스 제공자 : 동일한 기능을 하는 객체가 두개 만들어지는 것을 피하고 싱글톤으로 만들 필요가 있을 경우.
			```typescript
				providers: [주입할 클래스..]
			```

	선택적 장식자를 이용한 의존성 주입


	제공자 없이 객체 주입
