---
title: '스프린트 회고 && 요소의 움직임'
excerpt_separator: '<!--more-->'
categories:
  - CodeLion
tags:
  -
header:
  teaser: ./assets/image/7.png
toc: true
toc_sticky: true
toc_label: 'CONTENTS'
---

---

<br />

# 📚 What is TIL?

<!-- content -->

## `<a>` 과 `<button>`의 차이

### `<a>`

- 우클릭을 했을 시 다른 페이지 혹은 페이지 내의 특정 영역으로 이동 할 수 있는 메뉴가 보인다
- shift + click 했을 때 새로운 창으로 열린다
- 마우스오버, 포커스가 되었을 때 url 브라우저 창 하단에 노출된다

⚠️ href 값 없이 JS로 동작하게 하면 안된다  
⚠️ cursor:pointer 로 처리되는데 이것을 마우스커서의 모양 변경을 위해 사용되면 안된다
{:.notice--warning}

### `<button>`

- 여러 컨텐츠(이미지, 아이콘) 삽입할 수 있다
- ::before, ::after 와 같은 가상 요소를 사용할 수 있다

🔎 \<button> 과 달리 \<input>의 경우 빈태그 요소이기 때문에 value 특성에 텍스트 값 밖에 지정할 수 없다  
🔎 브라우저 기본동작 없기 때문에 JS를 이용하여 동작을 추가해야한다
{:.notice--info}

⚠️ \<li>, \<img>, \<span> 등 다른 태그에 JS 기능으로 버튼처럼 만들면 안된다  
{:.notice--warning}

💡 각 태그는 각자의 역할이 있다 역할에 맞게, 시맨틱하게 사용하자
{:.notice--primary}

<br>

## 동적 가상 선택자

<details>
<summary>더보기</summary><br>
<code>:active</code><br>
&nbsp;클릭시 활성화(누르고 있는 동안)<br>
  <br>
  <code>:visited</code><br>
&nbsp;사용자가 이미 방문한 링크일 경우 해당 상태에 만족합니다<br>
&nbsp;웹브라우저의 방문기록 정보를 사용합니다.<br>
  <br>
  <code>:disabled</code><br>
&nbsp;비활성화 된 요소를 선택합니다<br>
  <br>
  <code>:hover</code><br>
&nbsp;마우스 커서를 요소에 올려두었을 때<br>
  <br>
  <code>:focus</code><br>
&nbsp;focus 받은 상태를 나타냅니다<br>
  <br>
  <code>:checked</code><br>
&nbsp;input이 선택된 상태를 나타냅니다(checkbox radio 등)

</details>

### not disabled 되면서 hover을 주는 방법

```css
.btn:not(:disabled):hover {
  text-decoration: underline;
  color: #fff;
}
```

<br>

## 속성 선택자

<details>
  <summary>더보기</summary><br>
  <code>[속성이름]</code><br />
  &nbsp;해당 속성을 가진 요소 모두 선택<br />
  <br />
  <code>[속성이름<strong>~=</strong>"속성값"]선택자</code><br />
  &nbsp;특정 문자열로 이루어진 단어를 포함하는 요소를 모두 선택<br />
  <br />
  <code>[속성이름|="속성값"] 선택자</code><br />
  &nbsp;특정 문자열만 포함하거나, 특정 문자열로 시작하면서 바로 하이픈 <code>-</code> 기호가 있는 태그<br />
  <br />
  <code>[속성이름^="속성값"] 선택자</code><br />
  &nbsp;특정 문자열로 시작하는 요소를 모두 선택<br />
    <br />
  <code>[속성이름$="속성값"] 선택자</code><br />
  &nbsp;특정 문자열로 끝나는 요소를 모두 선택<br />
    <br />
  <code>[속성이름*="속성값"] 선택자</code><br />
  &nbsp;특정 문자열를 포함하는 요소를 모두 선택합니다.<br />
</details>

💡 속성 선택자가 양이 많기도하고 익숙하지 않아서 거의 쓰지 않아서...  
💡 여러개중 하나씩만 주로 쓰면서 연습해보자  
💡 `class^="btn"` 가 가장 많이 쓰일 것 같으니 먼저 써보며 익숙해지자
{:.notice--primary}

<br>

## transform

- 요소에 다양한 변형을 줄 수 있는 속성이다
- 요소의 회전, 스케일링, 왜곡 및 변환 뿐만 아니라 원근법 및 회전과 같은 3D 변환을 적용하는 것도 가능한 녀석이다...
- `scale` \| `rotate` \| `translate` <span class="smallText">(자신의 위치에서 x,y 축 이동이 가능)</span> \| `skew`

### translate 와 position 차이점

- translate 와 position 둘 다 요소의 위치를 조작하는 속성이다
- `translate` 는 다른 요소의 레이아웃에 영향을 주지않고 요소를 이동한다
- 반면 `position`은 부모 또는 뷰포트를 기준으로 요소의 위치를 지정하는 데 사용된다

💡 **정적** 인건 position **동적** 인건 transform을 사용하는 것이 좋다고 생각하자!
{:.notice--primary}

<span class="explain"> position이 바뀌면 레이아웃을 다시하고 페인트다시하고 다음단계에 영향이 미치는 ...? </span>

💡 브라우저 렌더링 꼭 공부해보자🙌
{:.notice--primary}

#### position으로 가운데 정렬 하는 법

```css
position: absolute;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

<br>

## transition

- 값의 변화가 일정 시간에 걸쳐 일어나도록 하는 것을 말한다
- `transition-property` \| `transition-duration` \| `transition-timing-function` \| `transition-delay`

🔎 **text-decoration:underline** 은 transition을 사용할 수 없다고 한다
{:.notice--info}

<br>

## animation

- `@keyframes` \| `animation-name` \| `animation-duration` \| `animation-timing-function`
- `animation-delay` \| `animation-iteration-count` \| `animation-direction` \ `animation-fill-mode`  
  <span class="explain">많다 많아.. 😵 요런게 있다 정도만...</span>

🔎 transition의 경우 **요소의 상태가 변경**되어야 애니메이션을 실행할 수 있다
{:.notice--info}

<br>

## 과제완성하면서 적용해보기..!

<br>

<img class="img" src="https://user-images.githubusercontent.com/96939334/224724167-d7ac7645-ad11-4bc2-9ca4-08422735e7da.gif">

<br>

마침 종찬님이 주신 과제를 하다가 오늘 배운 것을 조금이라도 적용해자는 생각에..!  
캐릭터의 이미지가 휙휙 돌면서 바뀌면 멋있겠다는 생각으로  
`transform`과 `transition`을 적용해보았다

텍스트를 이미지와는 다른 X축으로 돌려봤는데 생각보다 괜찮은거 같다 ㅎ  
사실 잘 작동할 줄 몰랐는데 잘 작동해서 기뻤다 👏

<details>
  <summary>코드보기</summary><br>
    <img src="https://user-images.githubusercontent.com/96939334/224781424-ca0aeb02-cbca-4a28-b72c-984feea7d1df.png">
    <img src="https://user-images.githubusercontent.com/96939334/224781429-6175ef87-1c29-4543-a8ac-a27549202257.png">
    <img src="https://user-images.githubusercontent.com/96939334/224781432-6c28d9a8-4b55-4038-8582-11d1c0f03f55.png">
   </details>

<br>

<br>

---

<br>

# ✨ Today is ...

## 첫 스프린트 회고

메이커준님과 스프린트 회고 진행을 하면서도  
깨닫는 부분이 많아서 그런지 특강같이 느껴졌다 👏

목표를 설정하고...  
달성했을 때와 달성하지 못했을 때를 떠올리며  
목표를 조금이나마 재설정하고...  
회고를 통해 앞으로 더 나아가기 위한 길을 바라볼 수 있는 기회를 가진 것 같다  
지금있는 기회 다시 오지 않을 수 있다 더 잘 활용해보자❗
