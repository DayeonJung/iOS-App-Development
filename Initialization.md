# Initialization

구조체와 클래스의 초기화

프로퍼티의 값 지정. 

# init()

자동으로 생성됨. 

# init()에서 반드시 해 주어야 하는 것들

- init이 끝나는 시점에는 모든 프로퍼티는 값을 가져야 한다.

클래스에는 convenience init(편의 초기화) 과 designated init(지정 초기화) 두 가지의 초기화가 존재한다.

- 지정 초기화는 부모클래스에 있는 지정 초기화를 호출해야 한다.
- 지정 초기화는 부모 클래스에 있는 편의 초기화를 호출할 수 없다!

- 클래스에서 우리가 만든 모든 프로퍼티를 초기화해야 한다. 부모 클래스의 init()을 부르기 전에!
- 부모 클래스의 프로퍼티에 접근하기 전에 부모클래스의 init을 호출해야 한다.
- convenience init은 그 클래스 내에서 다른 init함수를 호출할 수 있다. 부모클래스의 init을 호출할 수는 없음. 클래스 내의 프로퍼티에 접근하기 전에 반드시 그 init을 호출해야 한다.

# required init()

자식 클래스는 이 init을 반드시 실행해야 한다.