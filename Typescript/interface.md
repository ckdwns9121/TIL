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
    - 객체 리터럴은 다른 변수에 할당할 때나 인수로 전달할 때, 특별한 처리를 받고, 초과 프로퍼티 검사를 받는다.   
    - 만약 객체 리터럴이 "대상 타입"이 갖고 있지 않은 프로퍼티를 갖고 있으면, 에러가 발생한다.

```
    let mySquare = createSquare({color :"red", width:100});
```
이 검사를 피하는 방법은 타입 단언을 사용하는 것이다. (타입단언 : 컴파일러가 가진 정보를 무시하고 원하는 임의의 타입을 값에 할당하고 싶을 때 쓴다.)
```
    let mySquare = createSquare({width:100, opacity:0.5} as SquareConfig);
```
특별한 경우 추가 프로퍼티가 있을 시 인덱스 서명을 추가한다.

```
    interface SquareConfig{
        color?: string;
        width: number;
        [propName :string] : any;
    }
```
