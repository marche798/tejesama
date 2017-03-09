# 의존성 주입이란??
  - 의존성 주입(Dependency Injection) : 객체 조립과 설정을 위한 소프트웨어 디자인 패턴<br>
  - Angular 에서는 기본적으로 생성자 의존성 주입 패턴을 이용해 의존성을 주입 받음.<br>
```
	constructor(private speedmeter: Speedmeter, public engine:Engine) {
		.....
	}
```
  - Angular 의존성 주입 시 일어나는 중간 과정을 설정하거나 타입스크립트가 지원하지 못하는 인터페이스 형을 주입받게 하는 등 여러가지 제약을 극복할 방법을 제공.

