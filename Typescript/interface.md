# 인터페이스

- 첫 번째 인터페이스
    - 타입 검사는 printLabel 호출을 확인한다. printLabel 함수는 string 타입 label을 갖는 객체를 하나의 매게변수로 가진다.   
    이 객체가 실제로는 더 많은 프로퍼티를 가지고 있지만, 컴파일러는 최소한 필요한 프로퍼티가 있는지와 타입이 잘 맞는지만 검사한다.
    - LabeledValue 인터페이스는 label 프로퍼티 하나만을 가진다.
```
    function printLabel(labeledObj:{label:string}){
        console.log(labeledObj.label);
    }

    let myObj= {size:10 , label:"size 10 obj"} ;
    printLabel(myObj);
```

```
    interface LabeledValue{
        label: string;
    }

    function printLabel(labelObj :LabeledValue){
        console.log(labelObj.label);
    }

    let myObj = {size:10 , label:'size 10 obj'};
    printLabel(myObj);
```
   
- 선택적 프로퍼티
    - 인터페이스의 모든 프로퍼티가 필요한 것은 아니다. 어떤 조건에서 필요한 프로퍼티를 선택하여 쓸 수 있다.
    - 선택적 프로퍼티는 이름 끝에 ? 를 붙여 표시한다.
    - 선택적 프로퍼티의 이점은 인터페이스에 속하지 않는 프로퍼티의 사용을 방지하면서, 사용 가능한 속성을 기술하는 것이다.

```
    interface SquareConfig{
        color? : string;
        width? : number;
    }

    function createSquare(config : SquareConfig) : {color : string, area:number} {
        let newSquare = {color :"white" , area : 100};
        if(config.color){
            newSquare.color = config.color;
        }
        if(config.width){
            newSquare.are = config.width * config.width;
        }
        return newSquare;
    }

    let mySquare = createSquare({color:"black"});
```

- 읽기 전용 프로퍼티
    - 일부 프로퍼티들은 객체가 처음 생성될 때만 수정 가능해야한다. 프로퍼티 앞에 readonly를 넣어서 이를 지정할 수 있다.
    - const vs readonly = 변수냐 프로퍼티냐

```
    interface Point{
        readonly x: number;
        readonly y: number;
    }
```

- 초과 프로퍼티 검사
    -