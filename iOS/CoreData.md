# CoreData

CoreData는 Framework이다.

영구적으로 저장하기 위해 Persistence 기능을 많이 사용하지만 이는 CoreData의 기능중하나

코어 데이터는 Data base 보다 큰 개념

앱의 모델 계층, 객체 그래프를 관리하는 Framework이다.



## Core Data Stack

---

앱의 모델 layer를 관리하고 유지하는 역할을 한다.

### NSManagedObjectModel

+ Entity를 설명하는 DataBase 스키마 - 그냥 엔티티 어떻게 생겼는지 들고 있다고 보면 될듯

### NSPersistentStoreCoordinator

+ persistent storage와 managed object model을 연결해준다.

### NSManagedObjectContext

+ managed object 생성, 저장, 가져오는 등의 기능을 한다. 여기에 올려놓고 작업을 진행하기 때문에 보통 1개의 Context만 가지고 작업을 하는게 좋았다.

### NSPersistentContainer

+ Core Data Stack을 나타낼때 필요한 객체를 다 포함한다.



## 전체적인 흐름

---

1. NSPersistentContainer 컨테이너 생성 - CoreData 파일이랑 연결시켜준다.
2. Context 를 가져온다.
3. Entity를 가져온다.
4. NSManagedObject를 만든다.
5. NSManagedObject 인스턴스에 행할 행동을 해준다. (값 세팅 등등)
6. Context를 저장한다.

# User Defaults

작은 용량의 데이터를 사용하는데 용이하다.

key - value 쌍을 영구적으로 저장한다.



## 면접 질문

----

1. CoreData는 Thread Safe한가?
   + 아니다. 비동기적으로 CoreData의 읽고 쓰는 작업이 일어날 경우 race condition이 발생할 수 있다.
2. User Defaults는 Thread Safe한가?
   + 그렇다. [유저 디폴트 공식문서](https://developer.apple.com/documentation/foundation/userdefaults)

3. CoreData Persistence 기능이 어떻게 이루어지는지 설명해주세요
   1. CoreData Model 만들기
   2. Entity 만들기
   3. Entity에 필요한 attribute 추가
   4. 컨테이너 생성
   5. 컨테이너에서 Context 가져오기
   6. Entity 가져오기
   7. NSManagedObject를 만든다.
   8. NSManagedObject 인스턴스에 행할 행동을 해준다. (값 세팅 등등)
   9. Context를 저장한다.

