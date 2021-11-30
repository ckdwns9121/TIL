1. 타입추론
   TypeScript는 JavaScript의 언어를 알고 있으며 대부분의 경우 타입을 생성해준다. 예를 들어 변수를 생성하면서 동시에  
   특정 값에 할당하는 경우, TypeScript는 그 값을 해당 변수의 타입으로 사용한다.

```
    let helloworld = "Hello World!"
```

JavaScript가 동작하는 방식을 TypeScript가 이해함으로써 타입을 가지는 타입 시스템을 구축할 수 있다.  
이는 코드에서 타입을 명시하기 위해 추가로 문자를 사용할 필요가 없는 타입 시스템을 제공한다.
위 코드에서 TypeScript가 helloworld라는 변수가 string임을 알게되는 방식이다.

2. 타입정의

- name: string , id: number 을 포함하는 추론 타입을 가진 객체를 생성하는 코드

```
    const user ={
        name: "Hayes",
        id : 0,
    }
```

- 위 객체를 명시적으로 나타내기 위해서는 interface로 선언한다.

```
    interface User{
        name: string,
        id : number;
    }
```

- 변수 선언 뒤에 typename이 명시되어 새로운 interface 형태를 따르고 있다.

```
    interface User{
        name: string,
        id: number,
    };

    const user: User= {
        name :'Hayes",
        id : 0
    }
```

- 클래스로도 정의 가능하다.

```
    interface User{
        name : string,
        id:number,
    }

    class UserAccount {
        name: string;
        id:number ;

        constructor(name:string , id: number){
            this.name =name;
            this.id= id;
        }
    }
    const user:User = new UserAccount('hello',1);
```
