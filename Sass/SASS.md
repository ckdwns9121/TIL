# SASS

- SASS는 CSS pre-processor로서 , 복잡한 작업을 쉽게 할 수 있게 도와주고, 코드의 재활용성 및 가독성을 높여주어 유지보수가 용이하다.

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

### 5.1 mixin 활용

```
@mixin transition($transition...){
    -moz-transition : $transition;
    -o-transition : $transition;
    -webkit-transition : $transition;
    transition : $transition;
}

.move-button{
     @include transition(all 0.3s);
}

    // @each문으로 리스트 반복
@mixin transition($time){
    @each $prefix in -moz-, -o-, -webkit- ,''{
        #{$prefix}transition :$time;
    }
}
.move-button{
    @include transition(0.3s);
}
```

### 6. 조건문

- sass는 조건문을 사용할 수 있다.

```
$jb-type : jb-blue;
p{
    @if $jb-type== jb-red{
        color:red;
    }
    @else if $jb-type ==jb-blue{
        color:blue;
    }
    @else{
        color:black;
    }
}
```

### 7. 반복문

```
$i :1;
$gutter : 12px;

@while  $i<=10{
    .box-#{$i}{
        width : (60px * $i) + $gutter * ($i - 1);
    }
     $i : $i + 1;
} 

$total : 12;
@for $i from 1 to $total{
    .box-#{$i}{
        width : 70px * $i;
    }
}
```

### 8. 함수
- 함수는 mixin 과 비슷한 기능을 하지만 mixin은 style을 반환하고 함수는 값을 반환한다.

```
$wrap-width : 1000px;
@function set-width($n){
    @return $wrap-width /$n;
}
```

### 9. import (불러오기)

- 다른 파일의 스타일을 불러올 수 있다.
```
@import '../styles/root.scss';
```

### 10. extend (상속)

- 다른 스타일을 그대로 상속하여 다른 스타일을 추가할 수 있다.

```
.box{
    width : 50px;
    height :50px;
    }
.box2{
    @extend .box;
    border:1px solid red;
}
```
