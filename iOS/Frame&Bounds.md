# CGSize, CGPoint, CGRect

------

CGPoint - 2차원의 좌표계에서 점을 표현하는 구조체 (x,y 좌표 가지고 있음)

CGSize - 너비와 높이를 가지고 있는 구조체 (width, height 가지고 있음)

CGRect - 사각형의 위치와 크기를 가지고 있는 구조체 ( origin: CGPoint, size: CGSize 가지고 있음)

# Frame

------

superView를 기준으로 해당 view의 위치나 크기를 나타낸다.

# Bound

------

자기 자신을 기준으로 해당 view의 위치나 크기를 나타낸다.

**frame, bounds 모두 UIView의 instance property로 타입은 CGRect이다.**



## Origin, Size

---

+ Origin - x좌표, y좌표 즉 어디에 위치 해있는가?

+ Size - 크기, width, height

  

## clipsToBound

---

SubView가 내 View를 넘어간 경우 내 뷰 넘어로 SubView를 그릴지 말지 설정해주는 프로퍼티 기본값 false(밖으로 그려지는 가능)



## 차이점

------

Frame에 대한 개념은 바로 이해가 됐다. Bound의 origin이 변경되면 어떤일이 일어날까?

우리가 보고있는 view는 사실 엄청나게 큰 도화지로 생각해보자

그리고 화면에 나타나는 부분은 액자를 통해 보이는 극히 일부분이다.

액자의 위치를 바꾸면서 화면에 나타날 부분을 보여주는 것이다.

(0,0) → (20,20)으로 이동하게 된다면 액자의 위치가 20,20으로 이동하게 된다.

도화지 자체가 이동한것이 아니라 보여지는 액자의 위치가 변하기 때문에

(20,20)은 오른쪽 아래가 아닌 왼쪽 상단으로 view가 올라간것 처럼 보인다.

**결론적으로 바라보는 시점이 달라진다.**

**여기서 내가 말한 액자 개념이 ViewPort라고 한다.**



## 면접 질문

1. Frame과 Bounds에 대해 설명해주세요
   + Frame - superView를 기준으로 해당 view의 위치나 크기를 나타낸다.
   + Bounds - 자기자신을 기준으로 위치나 크기를 나타낸다.
2. Origin과 Size에 대해 설명해주세요
   + Origin - 위치
   + Size - 크기
3. 사각형 뷰를 45도로 돌렸을때 Frame과 Bounds의 변화에 대해 이야기 해주세요
   + Frame은 뷰를 감싸는 사각형 모양이다. 따라서 45도 돌아간 사각형을 감싸기위해 Frame의 size, origin 둘다 변할 가능성이 있다.
   + Bounds는 자기 자신의 상태를 나타내기 때문에 자신이 돌아간다해도 자기의 origin, size는 변함이 없다.
4. Frame은 언제 사용할까요?
   + 상위뷰위에 View를 어디에 어떤 크기로 걸건지 정할때 사용한다.
5. Bounds는 언제 사용할까요?
   + 자기 자신의 실제 크기를 알고 싶을때
   + 자신 안에 그림을 그릴때
   + 스크롤 할때 
6. Auto Layout은 Frame을 다룰까요 Bounds를 다룰까요?
   + 오토레이아웃은 뷰들간의 관계를 표현한다.
   + Frame-Based Layout : 특정 좌표로 뷰를 구성한다면 해상도가 다른 기기에서는 동일한 이미지로 안된다..
     Auto Layout : 제약조건에 따라 뷰계층 구조에 있는 모든 뷰의 크기와 위치를 동적으로 지정한다.
   + 오토레이아웃은 창틀끼리의 간격을 조정하고 창틀의 배치하고 창틀의 크기를 결정하는 것이라 frame을 다룬다.