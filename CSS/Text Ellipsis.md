# CSS에서 text ellipsis 처리하는 방법

- 한줄 라인 글자 수 제한 방법
- block레벨 태그에서만 적용가능

```
.text{
    width : 100px;
    padding: 0 5px;
    overflow : hidden;
    text-overflow : ellipsis;
    white-space : nowrap;
}
```

- 멀티라인 글자수 제한


```
.text{
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 3; /* 라인수 */
    -webkit-box-orient: vertical;
    word-wrap:break-word; 
    line-height: 1.2em;
    height: 3.6em; /* line-height 가 1.2em 이고 3라인을 자르기 때문에 height는 1.2em * 3 = 3.6em */
}

```

- Sass와의 응용법

```
// 멀티라인 말줄임 표시
// $line-cnt : 라인 수
// $line-height : line-height값
// 사용법 : @include ellipsis(3, 1.6em);
@mixin ellipsis($line-cnt, $line-height) {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: $line-cnt; 
    -webkit-box-orient: vertical;
    word-wrap:break-word; 
    line-height: $line-height;
    height: $line-height * $line-cnt;
}

.text{
    @include ellipsis(3,1.3em);
}

```