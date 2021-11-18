# 스켈레톤 UI 구성하기

```js
const SkeletonItem = () => {
  return (
    <div className="skeleton-item">
      <div className="skeleton-title-area">
        <div className="skeleton-image" />
        <div className="skeleton-title" />
      </div>
      <div className="skeleton-content" />
      <div className="skeleton-bottom" />
    </div>
  );
};
```

```scss
$skeleton-background: #f5f6f8;

@mixin skeleton-box($width, $height) {
  border: solid 1px #dfdfdf;
  width: $width;
  height: $height;
}

@mixin skeleton-content {
  content: ' ';
  width: 100%;
  height: 100%;
  position: absolute;
  left: -100%;
  top: 0;
  background: linear-gradient(
    to right,
    $skeleton-background,
    #aaa,
    #999,
    #aaa,
    $skeleton-background
  );
  animation: skeleton 2s;
  animation-iteration-count: infinite;
  opacity: 0.3;
}

@mixin skeleton-wrapper($height, $padding) {
  position: relative;
  width: 100%;
  height: $height;
  background-color: $skeleton-background;
  padding: $padding;
  border-radius: $padding;
  overflow: hidden;
  &::before {
    @include skeleton-content();
  }
}

@mixin skeleton-animation($blur) {
  @each $prefix in -moz-, -o-, -webkit-, -ms- {
    #{$prefix}filter: blur($blur);
  }
}

@keyframes skeleton {
  from {
    left: -100%;
  }
  to {
    left: 100%;
  }
}
```

```scss
.skeleton-item {
  @include mobile {
    width: 100%;
    max-width: none;
  }
  @include skeleton-wrapper(350px, 10px);
  width: calc(50% - 10px);
  margin-bottom: 20px;
  box-sizing: border-box;

  .skeleton-title-area {
    display: flex;
    .skeleton-image {
      @include skeleton-box(40px, 40px);
    }
    .skeleton-title {
      margin-left: 12px;
      @include skeleton-box(200px, 40px);
    }
  }
  .skeleton-content {
    margin-top: 12px;
    @include skeleton-box(100%, 230px);
  }
  .skeleton-bottom {
    margin-top: 12px;
    @include skeleton-box(100%, 36px);
  }
}
```
