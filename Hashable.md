# Hashable

### Hash란?

임의의 크기를 가진 데이터(key)를 고정된 크기의 암호화된 데이터(Value)로 변화시켜 저장하는 것.

**해시함수**(hash function)는 임의의 크기의 데이터를 고정된 크기의 데이터로 매핑하는 함수. 이 때 매핑 전 원래 데이터의 값을 키(key), 매핑 후 데이터의 값을 해시값(hash value), 매핑하는 과정을 해싱(hashing)이라고 함.

특정 입력에 대해 항상 같은 해시 값을 리턴하기 때문에 이를 이용해 인증이 가능. 어떤 입력인지 몰라도 해시함수를 이용해서 해시된 값이 일치하면 입력이 같다고 판단.

### Hashable이란?

정수 Hash값을 제공하는 타입. (애플 공식 문서)

Set 또는 Dictionary의 Key는 반드시 **Hashable을 준수하는 타입**이어야 함. 즉, 그 자체로 유일하게 표현이 가능해야 함.

Hashable 준수 타입 : Strings, integers, floating-point, Boolean values 등등.

**같은 타입의 인스턴스인 a와 b의 경우, a==b이면 a.hashValue == b.hashValue**

왜? Set, Dictionary Key는 Hashable 타입이어야 하는가?

해시 테이블이라는 자료구조 사용 시, 매우 빠른 데이터 검색을 하기 위해서! 

Set과 Dictionary가 중복을 허락하지 않는 이유이기도 함!

예를 들어, 0~10000까지 담을 수 있는 리스트 생성. "Hello"에 Hash 함수 적용. Hash값이 100이 나옴. 인덱스 100 위치에 "Hello"가 저장되어 있다. 그 다음에 "Hello"를 찾으려고 했을 때 바로 인덱스 100 위치로 가면 리스트의 앞에서부터 찾지 않아도 인덱스 100위치에 있는 "Hello"를 찾을 수 있다.

구조체의 경우, 저장프로퍼티는 모두 Hashable을 준수해야 한다.

열거형의 경우, 모든 associated values은 모두 Hashable을 준수해야한다. (associated values가 없는 열거형은 정의 없이(hashValue말하는듯) Hashable을 준수)