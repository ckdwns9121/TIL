# 마크다운 문법 정리

## 헤더

    큰제목 (======)
    작은제목 (------)
    #  H1
    ##  H2
    ###  H3
    ####  H4
    #####  H5
    ######  H6

### 순서있는 목록

    1. 첫번째
    2. 두번째
    3. 세번째

결과
1. 첫번째
2. 두번째
3. 세번째

### 순서없는 목록

    * 첫번째
      * 두번째
        * 세번째
    
결과

 * 첫번째
  * 두번째
  * 세번째

### 코드블럭

    This is a normal paragraph:

        This is a code block.
        
    end code block.

적용결과

    This is a normal paragraph:

        This is a code block.
    
    end code block.

- ```을 이용하는 방법

```javascript
    function test(){
        console.log('hello');
    }
```
### 링크

    참조링크:  [link keyword][id]
    외부링크:  [title][link]   ex [google](https://google.com ,"google link")

링크
    
### 수평선 hr 태그 사용

### 강조 표시를

```
    **강조**
```

### 이미지 사용법

```
![ex_screenshot](../이미지 경로)   
```

### 인용구 사용법

> 인용구 사용법은 이렇다

```
> 인용구1
>> 인용구2
>>> 인용구3
```

> 인용구1
>> 인용구2
>>> 인용구3
     

