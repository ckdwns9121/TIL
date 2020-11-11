# SASS

- Sass는 Css pre-processor로서 , 복잡한 작업을 쉽게 할 수 있게 도와주고, 코드의 재활용성 및 가독성을 높여주어 유지보수가 용이하다.

### 1. 변수선언

- 반복적으로 사용하는 값을 변수로 선언해서 사용.

```
    $red :  #000;
    $font-size : 12px;

```

### 2. Math Operators (수학 연산자)

- 단위를 계산해서 사용 가능
- 단 연산자를 사용할 때는 반드시 단위를 통일 시켜야 한다.
```
    width : 100% - 20px (x)
    이런 작업을 하려면 calc() 함수를 사용.
```

```
    width : 300px / 100px * 100% (o)
```

### 3. 내장함수

- sass에는 내장함수들이 있다.

[내장함수 오픈링크](http://jackiebalzer.com/color)

### 4. 중첩

- 코드를 블럭단위로 중첩시킬 수 있다.

```
    .container{
        
        h1{
            color:$color;
        }
    }
```


### 5.믹스인

- mixin은 sass에서 가장 많이 사용하는 문법이며 재사용성과 코드의 가독성을 높여준다.
- mixin으로 반복되는 구조의 틀을 잡아놓고 @include 지시자로 불러서 쓸 수 있다.

```
    //mixin 선언
    @mixin box{
        color:#000;
        width :100%;
        height: 100%;
        display:flex;
        flex-direction:column;
    }
    //mixin 사용
    .box{
        @include box;
    }

```

- mixin은 함수처럼 사용 가능. 

```
    //파라메터로 color와 width를 주고 값이 없을 시 초기화.
    @mixin box($color : #000, $width : 100%){
         color:$color;
        width :$width;
        height: 100%;
        display:flex;
        flex-direction:column;
    }

    .box{
        @mixin box();
    }
    .box2{
        @mixin box(#fff, 50%);
    }
```


