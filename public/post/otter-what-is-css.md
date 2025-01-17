---
id: 8
title: '[프론트엔드] CSS, 너는 무엇인가?'
date: '2023-02-09'
author: 'otter'
categories: 'front-end'
---

# 개요

> 📝 프론트엔드를 한다면 html과 더불어 같이 보게 되는 css, 이 css란 무엇일까?

---

# CSS

> **CSS(C**ascading **S**tyle **S**heets)
>
> Cascading : 계단식
>
> Style : 멋을 내다
>
> Sheets : (종이) 한 장

계단식으로 한 장에 **멋**이 무엇인가~ 를 정의하는 문서라고 볼 수 있다.

그래서 그 **멋**을 어디다 쓸 건데? 라고 물으신다면, 바로 **HTML 문서에 멋, 스타일**을 더해주는 것이다.

HTML이 정의한 친구들에게 요소의 색상, 크기, 레이아웃, 폰트 등 다양한 스타일을 입혀줄 수 있다.

<img src="../assets/CSS.png" width="300"/>

**CSS**는 **선택자**와 **선언 구역**으로 구성된다.

**선택자(Selector)**는 스타일을 적용할 HTML 요소를 선택하는 역할을 맡고 있다.

요소를 선택한 후, 중괄호로 선언 구역을 설정한 후, 그 안에 스타일을 지정해준다.

선언 구역에서 **스타일 종류(속성) : 스타일 값**으로 스타일을 선언해주면 HTML에서 그 구역을 보고 적용시킬 것이다.

<figure>
    <img src="../assets/CSS_wtf.gif" width="300"/>
    <figcaption>CSS 적용 시 흔히 발생하는 일.gif</figcaption>
</figure>

---

## Cascading

CSS에서 가장 앞의 단어인 **Cascading**은, 폭포, 위에서 아래로 쏟아지는 이라는 뜻을 가진 단어이다.

말 그대로 **위에서 아래로 적용되는 스타일 시트**라는 건데… **그래서?**

CSS을 작업하다보면, 여러 스타일 규칙이 한 요소에 적용되기도 하고, 적용될 수도 있다.

그럴 때 **우선순위**가 필요한데, 그 우선순위를 결정하는 방식을 **CSS cascading**이라고 하는 것이다.

중요한 스타일 적용 규칙이기 때문에 제대로 이해하지 못하고 남발한다면, 위의 짤방처럼 웃픈 일이 발생된다.

<figure>
    <img src="../assets/loopy_shit.jpeg" width="300"/>
    <figcaption>X발</figcaption>
</figure>

~~(아는 사람 얘기다.)~~

CSS Cascading은 다음 3가지에 의해 결정된다.

- 중요도 : CSS가 어디서 선언됐는지
- 명시도 : 선택자 특정성의 중요도가 높은지
- 선언 순서

---

<img src="../assets/important.gif" width="300"/>

### 중요도

1. HTML의 head 요소 안의 style

   이 부분에 정의된 스타일은 해당 HTML 파일 내의 요소에 직접적으로 적용된다.

   ```html
   <head>
     <style>
       p {
         color: blue;
       }
     </style>
   </head>
   ```

2. HTML의 head 요소 안의 style 내부의 @import 문

   다른 CSS 파일을 가져와서 스타일을 정의할 수 있는데, 렌더링 성능에 영향을 줄 수 있기 때문에 가급적 사용을 피하는 것이 좋다.

   ```html
   <head>
     <style>
       @import url('styles.css');
     </style>
   </head>
   ```

3. `<link>`로 연결된 CSS 파일

   HTML 문서에 외부 CSS 파일을 연결하는 표준 방법이다. 가장 많이 사용하는 방법이 아닐까 싶다.

   ```html
   <head>
     <link rel="stylesheet" type="text/css" href="styles.css" />
   </head>
   ```

4. `<link>`로 연결된 CSS 파일 내부의 @import 문

   외부 css 파일 내에서 다른 css 파일을 가져오는 것이므로 그닥 좋지 못하다.

5. 브라우저 디폴트 스타일 시트

   자체적으로 브라우저가 가지고 있는 기본적인 스타일 시트를 뜻한다.

   ```css
   /* 헤더 태그의 기본 스타일 */
   h1,
   h2,
   h3,
   h4,
   h5,
   h6 {
     font-weight: bold;
   }
   ```

---

<img src="../assets/clarity.gif" width="300"/>

### 명시도

명시도는 CSS 규칙이 어떤 순서로 우선권을 갖는지를 결정하는 방식이다. 이름 옆에 쓰여진 것은 명시도 점수다.

1. !important

   이름부터 중요하다…! 근데, 쓸 때 정말 잘 생각해서 써야한다. 강제로 이 스타일을 우선시 해!의 느낌이라…

   ```css
   p {
     color: red !important;
   }
   ```

2. inline 스타일 : **1000점**

   important는 예외라고 생각하고, 이 inline 스타일이 가장 높은 우선순위라고 생각하면 된다.

   ```css
   <p style="color: blue;">This is a paragraph.</p>
   ```

3. id 선택자 : **100점**

   html 태그 내의 id는 `#`으로 선택한다.

   ```css
   #unique-paragraph {
     color: green;
   }
   ```

4. class / 가상 선택자 : **10점**

   html 태그 내의 class는 `.`으로 선택하고, 가상 선택자는 `:`으로 선택한다.

   [가상 선택자](https://developer.mozilla.org/ko/docs/Web/CSS/Pseudo-classes)는 가상 이벤트를 뜻하는데, :link, :visited, :focus 등 다양하다.

   ```css
   .button {
     color: yellow;
   }

   .button:hover {
     background-color: orange;
   }
   ```

5. 태그 선택자 : **1점**

   태그 선택자는 우선순위가 낮다.

   ```css
   p {
     color: purple;
   }
   ```

6. 상속된 스타일

   부모 요소로부터 상속된 스타일은 직접 스타일이 명시된 것이 아니기 때문에 가장 명시도가 낮다.

   ```html
   <!doctype html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Inheritance Example</title>
       <style>
         .parent {
           color: blue; /* 부모 요소의 텍스트 색상을 파란색으로 설정 */
         }
       </style>
     </head>
     <body>
       <div class="parent">
         <!-- 부모 요소 -->
         <p>This is a paragraph with inherited color.</p>
         <!-- 자식 요소 -->
       </div>
     </body>
   </html>
   ```

---

<img src="../assets/declare.webp" width="300"/>

### 선언 순서

늦게 선언된 스타일이 우선 적용된다.

```css
/* 첫 번째로 선언된 스타일, 적용X */
.box {
  color: red;
}

/* 두 번째로 선언된 스타일, 적용됨 */
.box {
  color: blue;
}
```

### Cascading 예시

```html
<div id="container" class="box">
  <p class="box">Hello, world!</p>
</div>
```

```css
.box {
  color: blue; /* 클래스 선택자, 10점 */
}

#container p {
  color: red; /* 아이디 선택자 + 태그 선택자, 101점 */
}

.box {
  color: green; /* 클래스 선택자, 10점 */
}
```

<img src="https://github.com/SanGyuk-Raccoon/SanGyuk-Raccoon.github.io/assets/144116866/0e6290f6-2cfa-4916-a208-35e3f4926ff2" width="300"/>

이런 코드에서는, `#container p`가 우선적용 될 것이다. 못 믿겠으면 한번 직접 해보자!

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Declaration Order Example</title>
    <style>
      /* 첫 번째로 선언된 스타일 */
      .box {
        color: red;
      }

      /* 두 번째로 선언된 스타일 */
      .box {
        color: blue;
      }
    </style>
  </head>
  <body>
    <div class="box">Hello, world</div>
  </body>
</html>
```

아래 코드로는 당연히 blue가 적용될 것이다.

---

<img src="https://github.com/SanGyuk-Raccoon/SanGyuk-Raccoon.github.io/assets/144116866/0c808e40-0b5a-4e6a-852a-4f36bd194220" width="300"/>

Cascading 규칙이 어렵고, 직관적이지 못하다면 [해당 사이트](https://specificity.keegan.st/)를 이용해보자.

이름을 바꾸고, 우측 상단에 `Sort by specificity`를 누르면 자동으로 정렬해주는 마법사같은 친구다.

선택자들을 입력할 수도 있고, 선택자에 따른 점수도 표기되니 헷갈릴 때 유용하게 사용할 수 있을 것 같다.

💡 본 포스팅에 대한 지적, 문의는 언제든지 환영입니다.
