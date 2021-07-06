# Box-Sizing 속성에 대해 알아보자

- box-sizing은 박스의 크기를 어떤 기준으로 계산할 지 정하는 속성
- 기본값 : content-box


### content box

- 지정한 CSS width 및 height를 컨텐츠 영역에만 적용한다.
- border, padding, margin은 따로 계산되어 전체 영역이 설정값보다 커질 수 있다.

### border box
- 지정한 CSS width 및 height를 전체 영역에 적용한다.
- border, padding, margin을 모두 합산하기 때문에 컨텐츠 영역이 설정 값 보다 작아질 수 있다.

