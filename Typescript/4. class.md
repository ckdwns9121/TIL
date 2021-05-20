# 클래스

1. 클래스
```
    class Greeter{
        greeting:string;
        constuction(message: string){
            this.greeting = message;
        }
        greet(){
            return "Hello" + this.greeting;
        }
    }

    let greeter = new Greeter("world");
```

2. 상속
    - TypeScript에서는 , 일반적인 객체지향 패턴을 사용할 수 있다.
    - 파생된 클래스의 생성자는 기초 클래스의 생성자를 실행할 super()를 호출해야 한다.

```
    class Animal{
        move(distanceInMeters : number=0){
            console.log(`Animal moved ${distanceInMeters}m.`);
        }
    }
    class Dog extends Animal{
        bark(){
            console.log('woof ! woof!');
        }
    }
    const dog = new Dog();

    dog.bark();
    dog.move(10);
    dog.bark();
```

```
        class Animal {
            name: string;
            constructor(theName: string) { this.name = theName; }
            move(distanceInMeters: number = 0) {
                console.log(`${this.name} moved ${distanceInMeters}m.`);
            }
         }

        class Snake extends Animal {
            constructor(name: string) { super(name); }
            move(distanceInMeters = 5) {
                console.log("Slithering...");
                super.move(distanceInMeters);
            }
        }

        class Horse extends Animal {
            constructor(name: string) { super(name); }
            move(distanceInMeters = 45) {
                console.log("Galloping...");
                super.move(distanceInMeters);
            }
        }

        let sam = new Snake("Sammy the Python");
        let tom: Animal = new Horse("Tommy the Palomino");

        sam.move();
        tom.move(34);
```

- 접근지정자 public
    - public 
    - public은 생략가능 기본적인 접근지정자는 public

```
    class Animal {
    public name: string;
    public constructor(theName: string) { this.name = theName; }
    public move(distanceInMeters: number) {
        console.log(`${this.name} moved ${distanceInMeters}m.`);
    }
    
    }
```
- ECMAScript 비공개 필드
    - TypeScript 3.8에서 비공개 필드를 위한 JavaScript의 새로운 문법을 지원한다.

```
    class Animal {
    #name: string;
    constructor(theName: string) { this.#name = theName; }
}

    new Animal("Cat").#name; // 프로퍼티 '#name'은 비공개 식별자이기 때문에 'Animal' 클래스 외부에선 접근할 수 없습니다.
```

- 접근지정자 private & protected
    - private : 파생클래스에서도 접근 불가
    - protected : 파생클래스는 접근 가능


- 접근자 getter setter
    - TypeScript는 객체의 멤버에 대한 접근으로 getter/setter를 지원한다

```
    class Employee{
        private fullName : string;

        get fullName() :string{
            return this.fullName;
        }
        set fullName(name : string){
            this.fullName = name;
        }

    }
    let employee = new Employee();
    employee.fullName = "bob";
    if(employee.fullName){
        console.log(employee.fullName);
    }
```


- 추상클래스 Abstract
    - 추상 클래스는 다른 클래스들이 파생 될 수 있는 기초 클래스이다.
    - 추상 클래스는 직접 인스턴스화 할 수 없다.
    - 추상 클래스는 인터페이스와 달리 멤버에 대한 구현을 세부화 할 수 있다.
    - abstract 키워드는 추상 메서드를 정의할 때도 사용한다.

```
    abstruct class Animal{
        absctuct makeSound(): void;
        move() : void{
            console.log('move');
        }
    }
```

```
    abstract class Department {

    constructor(public name: string) {
    }

    printName(): void {
        console.log("Department name: " + this.name);
    }

    abstract printMeeting(): void; // 반드시 파생된 클래스에서 구현되어야 합니다.
    }

    class AccountingDepartment extends Department {

        constructor() {
            super("Accounting and Auditing"); // 파생된 클래스의 생성자는 반드시 super()를 호출해야 합니다.
        }

        printMeeting(): void {
            console.log("The Accounting Department meets each Monday at 10am.");
        }

        generateReports(): void {
            console.log("Generating accounting reports...");
        }
    }

    let department: Department; // 추상 타입의 레퍼런스를 생성합니다
    department = new Department(); // 오류: 추상 클래스는 인스턴스화 할 수 없습니다
    department = new AccountingDepartment(); // 추상이 아닌 하위 클래스를 생성하고 할당합니다
    department.printName();
    department.printMeeting();
    department.generateReports(); // 오류: 선언된 추상 타입에 메서드가 존재하지 않습니다
```