# 의존성 주입이란??
 의존성 주입(Dependency Injection) : 객체 조립과 설정을 위한 소프트웨어 디자인 패턴<br>
 Angular 에서는 기본적으로 생성자 의존성 주입 패턴을 이용해 의존성을 주입받는다.
```
	constructor(private speedmeter: Speedmeter, public engine:Engine) {
		.....
	}
```

