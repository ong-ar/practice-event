# event

## 이벤트 버블링

```html
<div onclick="alert('div1')">
  div1
  <div onclick="alert('div2')">
    div2
    <div onclick="alert('div3')">div3</div>
  </div>
</div>
```

또는

```html
<div class="div1">
  div1
  <div class="div2">
    div2
    <div class="div3">div3</div>
  </div>
</div>
```

```javascript
var divs = document.querySelectorAll("div");
divs.forEach(function(div) {
  div.addEventListener("click", logEvent);
});

function logEvent(event) {
  alert(event.currentTarget.className);
}
```

실행 결과

    alert: div3 -> div2 -> div1

<sup>div3 클릭 시</sup>

엘리먼트에서 이벤트가 감지되면 해당 엘리먼트를 포함하고 있는 부모 엘리먼트를 통하여 최상위까지 이벤트가 전달되는 것  
예외적으로 focus 는 버블링이 없음

`event.target`: 최초 이벤트 엘리먼트  
`event.currentTarget`: 실제 이벤트 실행 엘리먼트

## 이벤트 캡처링

```html
<div class="one">
  div1
  <div class="two">
    div2
    <div class="three">div3</div>
  </div>
</div>
```

```javascript
var divs = document.querySelectorAll("div");
divs.forEach(function(div) {
  div.addEventListener("click", logEvent, {
    capture: true // default 값은 false입니다.
  });
});

function logEvent(event) {
  alert(event.currentTarget.className);
}
```

실행 결과

    alert: div1 -> div2 -> div3

<sup>div3 클릭 시</sup>

엘리먼트 이벤트 발생 시 최상위부터 해당 엘리먼트까지 이벤트 전달  
구현 방법은 `addEventListener` 두번째 파라미터에 `capture: true` 추가

## event.stopPropagation()

```javascript
function logEvent(event) {
  event.stopPropagation();
  alert(event.target.className);
}
```

해당 엘리먼트 이벤트 호출하고 싶다면 `event.stopPropagation()` 사용

## 이벤트 위임

```html
<div class="div1">
  <div class="div2">
    <input type="checkbox" class="input1" />
    <input type="checkbox" class="input2" />
  </div>
</div>
```

```javascript
var inputs = document.querySelectorAll("input");
inputs.forEach(function(input) {
  input.addEventListener("input", logEvent);
});

function logEvent(event) {
  alert(event.currentTarget.className);
}
```

- 만약 체크박스가 추가되면 이벤트를 새로 만들어줘야되는 문제점이 있다.

```javascript
var div2 = document.querySelector(".div2");
var input = document.createElement("input");
input.setAttribute("type", "checkbox");
input.setAttribute("class", "input3");
div2.appendChild(input);
```

- 해결 방법은 버블링을 이용하면 된다. 부모 엘리먼트에 이벤트 리스너를 추가하면 된다.

```javascript
var parentDiv2 = document.querySelector(".div2");
parentDiv2.addEventListener("click", logEvent);
```
