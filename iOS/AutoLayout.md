# Auto Layout

뷰에게 어떤 조건이나 명령을 줘서 변화에 대응하도록 하게 해준다.



## Auto Layout 의 목적

---

제약을 제시하여 자신의 위치나 크기를 찾아가게 해준는 것

**어떤 제약이 누락되거나 잘못 되면 전체가 무너질 가능성이 있다.**



## 뷰가 변하는 외부적 요인?

---

1. 사용자가 윈도우 사이즈를 조정

2. 아이패드의 스플릿 뷰

3. 기기가 rotate 되었을 때

4. 전화가 오거나 레코딩바 같은 특수 화면이 생기고 사라질때

5. 사이즈 클래스를 통해 스크린 사이즈에 따라 지원 할 때

   

## 뷰가 변하는 내부적 요인?

---

1. 앱 안에서 사용자의 응답에 따른 변화(누르면 커지는 버튼)
2. Dynamic type에 따른 변화



## >= <= 등이 포함된 제약?

---

1. 버튼의 크기가 오른쪽 제약을 500을 주면 찌그러진다.
2. 이때 500만큼 Less Than or Equal을 주게되면 조건 500보다 작아 질 수 있게된다.
3. 버튼이 찌그러지지 않고 제대로 보인다.



## Constraint Priorities

---

제약의 우선도

+ 여러개의 제약이 동시에 들어오면 우선도가 높은 제약이 먼저 적용된다.
+ 100보다 작거나 같으면 좋겠다 vs 20으로 했으면 좋겠다 
+ 양쪽의 조건을 실행할 녀석을 우선순위를 높게 주면 된다.



## Intrinsic Content Size

------

고유 컨텐츠 사이즈

컨텐츠의 사이즈를 기반으로 뷰의 사이즈를 조정할 수 있다.

ex) 버튼안에 있는 text의 크기를 기반으로 버튼의 사이즈 확정이 가능

+ Label, Button, 등 거의 intrinsic size가 존재한다.
+ Custom View는 존재하지 않다.
+ Text View, image View 는 매우 변화가 다양하여 존재하지 않다.

### 어떤 차이일까?

Label, button등의 경우 실제 크기를 지정해주지 않고 top, leading만 주더라도 잘 동작한다.

View의 경우에는 top, leading만 지정해주면 실제 크기를 알 수 없기때문에 에러 발생

위와 같은 메서드로 View에 Intrinsic Content Size 부여가 가능하다.

```swift
override var intrinsicContentSize: CGSize {
	return CGSize(width: 50, height: 50)
}
```



## CH CR

---

+ Content resistance: 외부에서 누를때 버티는 힘

+ Content hugging: 늘어나지 않으려고 하는 힘

  

**언제 사용할까?**

경험상 스택뷰안에 있는 친구들을 처리할 때 많이 사용했다.

ex) Label 3개가 연달아 있다면...

Label은 늘어날 가능성이 있다. 만약 늘어나서 서로 충돌을 하게되면 어느 것이 줄어들지 모르는 상황

널널한 상황이면 누가 늘어나야 하는지 모르는 상황



+ hugging priority를 높여주면 늘어나지 않으려는 힘이 강해짐

+ resistance priority를 높여주면 쪼그라들지 않으려는 힘이 강해짐



## Safe Area

---

iOS 11 이전에 Top/Bottom Layout Guide가 존재했었다.

상태바, 네비게이션바, 탭바 등에 의해 View가 가려지지 않도록 필요했었다.



**하지만 노치가 등장**



노치가 등장하고 나서 핸드폰이 LandScape 상태일 때 leading, trailing의 마진이 필요하게 되었다.

따라서 Top/Bottom Layout Guide에서 Safe Area로 넘어가게 되었다.



## 면접 질문

---

1. Auto Layout이란 무엇인가요?
   + 뷰에게 제약을 제시하여 자신의 위치와 크기를 알게하고 변화에 대응하도록 해주는 것
2. Hugging, resistance에 대해서 설명해주세요
   + Hugging은  늘어나지 않으려는 힘
   + Resistance는 쪼그라 들지 않으려는 힘
3. Intrinsic Size에 대해서 설명해주세요
   + 자기 자신이 가지고 있는 Content를 통해 뷰의 크기가 결정될 수 있다.
   + 예를 들면 Button에 들어있는 Text를 통해 자신의 크기를 결정 지을 수 있다.
   + Custom View, Image VIew, Text View는 Intrinsic Size를 기본적으론 가지고있지 않다.
4. 오토레이아웃을 코드로 작성하는 방법은 무엇일까요?
   + 제가 주로 사용하는 방법은 Layout Anchor를 통하여 제약조건을 결정하는 방법
   + 그 외에 NSLayoutConstraint Class, Visual Format Language를 이용한 방법이 있다.
5. 스토리 보드를 이용했을때의 장단점이 무엇인가요?
   + 장점
     + 화면이 눈에 보이기 때문에 직관적으로 뷰의 구성이 가능하다.
   + 단점
     + 협업이 어렵다 - 같은 스토리 보드에서 동시에 작업이 일어나면 Merge Conflict를 해결하기 어려움
     + 개인적으로 아기자기 하게 gui를 이용해서 만지는거 자체가 난 별로였음 -ㅅ-
     + 재사용하기가 힘들다.
6. Safe Area가 뭔가요?
   + 기존에 탑 바텀 레이아웃 가이드가 있었지만 노치가 생기면서 핸드폰이 가로 모드 일때 화면을 가리는 현상이 발생
   + 이를 해결하기위해 탑 바텀 레이아웃을 디플리케이트 시키고 상하좌우에 전부 마진을 주기 위해 생겨난 공간이 Safe Area
7. Left Constraint 와 Leading Constraint 의 차이점이 무엇인가요?
   + leading - 글자가 시작하는 지점 왼쪽이 아니다.
   + left - 화면의 왼쪽
   + Localization에 필요한 개념이다. 특정 국가의 언어는 오른쪽에서 시작하는 경우가 있기 때문에 이를 맞추기 위해 leading을 주로 사용했었다.