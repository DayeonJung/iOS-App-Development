# array 내 .map이나 .filter 를 사용하는가?

### `lazy` 속성을 활용할 수 있는 지 확인한다.

```swift
let count = stages.lazy.filter{ $0 == stage }.count
```

`lazy` 속성을 활용하게 되면 array가 처리되는 방식이 변경된다. 

lazy를 사용하지 않으면, array의 모든 원소에 filter가 처리되며 새로운 array에 결과를 저장한다. 

하지만 lazy를 사용하면, sequence나 collection의 값이  down stream functions에서 요청시에 생성된다. 값들은 어떤 배열에도 저장되지 않고 필요할 때만 생성된다.

```swift
// lazy를 적용하지 않았을 때
[1, 2, 3, -1, -2].filter({ print("filtered one"); return $0 > 0 })
	.reduce(0) { (total, elem) -> Int in 
		print("counted one") 
		return total + 1 
}
```

```swift
filtered one
filtered one
filtered one
filtered one
filtered one
counted one
counted one
counted one
```

```swift
// lazy를 적용했을 때
[1, 2, 3, -1, -2].lazy.filter({ print("filtered one"); return $0 > 0 })
	.reduce(0) { (total, elem) -> Int in 
		print("counted one")
		return total + 1 
}
```

```swift
filtered one
counted one
filtered one
counted one
filtered one
counted one
filtered one
filtered one
```

### 언제 lazy를 쓸까?

1. 작업을 연결할 때 사용한다. 예) filter 후 reduce를 할 때
2. 스토리지에 할당하지 못하도록 방지할 때
3. down stream process가 더 빨리 시작되길 원하고 upstream process가 모든 작업을 먼저 수행할 때까지 기다릴 필요가 없는 경우.