
프레임워크 패턴의 장점 : 화면에 보여주는 로직과 실제 데이터가 처리되는 로직을 분리.

# MVVM
**M**odel

**V**iew

**V**iew **M**odel - View를 표현하기 위해 만들어진 View를 위한 Model


MVVM은 두가지 디자인 패턴을 사용. 
**Command**패턴과 **Data Binding**.

이 두가지 패턴으로 인해 View와 ViewModel은 의존성이 완전히 사라지게 된다.

MVP와 마찬가지로 View에서 입력이 들어온다. 
입력이 들어오면 Command 패턴을 통해 ViewModel에 명령을 내리게 되고 Data Binding으로 인해 ViewModel의 값이 변화하면 바로 View의 정보가 바뀐다.

View 클래스가 Model 클래스를 인식하지 못하도록 해야 한다.
View Model에서만 Model 클래스를 알고 있어야 한다. View와 View Model은 양방향 바인딩이 이루어진다.
뷰와  뷰모델은  변경이  되었을  때, 서로  변경이  되었음을  알려준다.

Model(테스트할 데이터를 입력)과 View Model로 Unit Test가 쉬워진다.


**정리!**
1.  View에 입력이 들어오면 Command 패턴으로 ViewModel에 명령.
2.  ViewModel은 필요한 데이터를 Model에 요청.
3.  Model은 ViewModel에 필요한 데이터를 응답.
4.  ViewModel은 응답 받은 데이터를 가공해서 저장.
5.  View는 ViewModel과의 Data Binding으로 인해 자동으로 갱신.




ex) MVVMSample 
```
struct  Info {
	let name: String
	let age: Int
}
```
1. ViewModel에 멤버변수를 생성하여 Model의 변수를 바인딩하도록 의존성 주입.

```
struct  InfoViewModel {
	let name: String

	init(info: Info) {
		self.name = info.name
	}
}
```


2. ViewController에 뷰모델 멤버변수(CourseViewModel) 생성
```
class  ViewController: UIViewController {

	var  infos = [InfoViewModel]()
	
}
```

3. 통신하면서 받아오는(어찌됐든 tableview cell에 전달할) 객체를  뷰모델  객체로  변환하여  바인딩

```
override  func  viewDidLoad() {
	let infosArr = [Info(name: "나강남", age: 12), Info(name: "김일구", age: 67), Info(name: "차정원", age: 26)]
	self.infos = infosArr.map({ return InfoViewModel(info: $0)})
}
```
4. View(cell)에 ViewModel 타입의 멤버변수 생성한 후 didSet으로 Label.text 등과 같은 세팅하기
**ViewModel 값으로 바인딩!!**

```
var  infoViewModel: InfoViewModel! {
	didSet {
		self.lbName.text = infoViewModel.name
	}
}
```
5. View Controller의 cellForRowAt에서 View(cell)의 ViewModel변수에 데이터 전달. 
```
cell.infoViewModel = self.infos[indexPath.row]
```

6. ViewModel에 Model의 멤버변수를 처리하여 ViewModel의 멤버변수로 저장하고, 실제 적용은 View에서 ViewModel값을 바인딩하여 사용한다.
```
struct InfoViewModel {
	let name: String
	let ageText: String //추가

	init(info: Info) {
		self.name = info.name
		self.ageText = info.age >= 50 ? "50대 이상" : "50대 미만" //추가
	}
}
```

```
class  InfoCell: UITableViewCell {

	var  infoViewModel: InfoViewModel! {
		didSet {
			self.lbName.text = infoViewModel.name
			self.lbAge.text = infoViewModel.ageText //추가
		}
	}
}

```
