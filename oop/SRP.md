# SRP

# 클린 코더스 강의 13. SRP(Single Responsibility Principle)

* 강의 보고 정리
* [강의 링크](https://www.youtube.com/watch?v=AdANHDp5dTM&t=714s)
## Responsibility

<p align="center">
	<img src="https://i.imgur.com/LJMfQTW.png">
</p>

* 클래스는 하나의 책임을 가져야한다
* 책임은 무엇인가 ?


* save/findById - 디비에 데한 접근 같은 부류
* 같은 책임을 갖는 기능 - calculatePay
  - calculateDeuction, calculateSalary
  - 추가핻 책임의 수는 변하지 않음
  - 메소드가 추가한다고 해도 그 수만큼 책임이 증가하는 건아님
* 부류
  - 메소드의 client에의해 결정
  - ***누가 해당 메소드의 변경을 유발하는 사용자인가?***
    - `save` 메소드에 변경이 필요하면 누구 때문에 변경되는 것인가

## It`s About Users

* SRP는 사용자에 과한것
* 책임
  - SW의 변경을 요청하는 특정 사용자들에 대하 클래스 / 함수가 갖는 것
  - ***"변경의 근원"*** 으로 볼수 있음

## It`s About Users
<p align="center">
	<img src="https://i.imgur.com/jB1w4ei.png">
</p>

* Employee 클래스의 변경을 요구하는 사용자들
  - Actor: 서로 다른 Needs, 서로다른 요구 사항, Expectation을 가짐

## It`s About Roles
<p align="center">
	<img src="https://i.imgur.com/jB1w4ei.png">
</p>
* User들은 그들이 수행하는 Role에 따라 나눠야 한다
* USer가 특정 Role을 수행할 때 Actor 라고 부른다.
  - 책임은 개인이 아니라 액터와 연결
* Employee 클래스에는 3 개의 액터가 있다
  - Policy, Architect, Operations

## Rerise

* Responsibility
 * Actor의 요구사항 변경이 일련의 함수들의 변경의 근원이 된다.

## Two Values of SW


## Collision
![](https://i.imgur.com/2o71S7u.png)
* Primay Value 저하
  - Policy Actors: 비지니스 룰의 변경을 필요함
  - ArchiterCure Actors: DB 스키마 변경을 필요함
  - 동일 모듈의 변경, Merge 충돌 Source Repo 충돌

## Fan Out
* 임플로이는 너무 많으것을안다
  - 비니지스 룰
  - 디비
  - 리포트, 포멕팅
* 많은 책임을 갖는다
* 각각  책임은 임플ㄹ이가 다른 클래스들을 사용하도록 한다.


## Fan Out
![](https://i.imgur.com/hNlfrQF.png)

* 변경에 민감
* Fan Out을 제한하는 것이 좋다
  - 좋은 방법은 책임을 최소하하는 것

## SRP
* 모듈은 하나/반드시 ***하나의 변경 사유*** 를 가져아한다
  - 변경 사유 : 액터
  - 액터 : 그 클래스를 사용하는 사람
  - **하나의 클래스는 한 종류의 클라이언트만 서빙 해야한다.**
* One and only one responsibility
  - 동일한 이유로 변경되어야 하는 것들은 동일 모듈에
  - 다른 이유로 변경되어야하는 것들은 다른 모듈에

## Solutions
![](https://i.imgur.com/SOEJMlG.png)

* 3개의 Actor, 3개의 Responsibility이 하나의 클래스
* 어떻게 Responsibility를 분리하나 ?

## Inverted Dependencies ID
![](https://i.imgur.com/vh2rK5X.png)

* OOP에서 이런 의존성을 다루는 전략
  - 클래스를 인터페이스와 클래스로 분리
*  Actor를 클래스에서 Decouple
  - 모든 Actor들이 하나의 인터페이스에 분리
  - 하나의 클래스에 구현되어 그햔더 분리

* 클래스가 변경되더라도 인터페이스가 변경되지 않으면 액터들이 변경되지 않음
  - 인터페이스가 변경되면 모든 클래스가 변경 되긴 함...
  - 하지만 레거시를 다루기에는 정말 좋다
  - 우리 시스템에 도입하면 좋을 거같다. IDE 에서 Extract Interface 자동으로 해줌

## Extract Classes
![](https://i.imgur.com/lwML6FJ.png)

* 3개의 책임을 분리하는 방법 : 3개의 클래스로 분리
* 결과
  - Actor들을 분리된 3개의 클래스에 의존
  - 3개의 책임에 대한 구현은 분리
  - 하나의 책임의 변경에 따른 책임에 영향 안미침
* 문제점
  - 임플로이 개념이 3개의 조각으로 분리

## SRP의미
* 한 모듈이 하나의 엑터를 위한 책임을 갖도록 분리하는 설계를 하는 것이 의미를 가짐
* 나는 늘 에거를 찾고 이에 기반하여 모듈을 분리한다.