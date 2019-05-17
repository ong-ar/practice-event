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

## 이벤트 캡처

## 이벤트 위임
