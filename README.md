# Transform card
*Посмотреть демо [на Codepen](https://codepen.io/AlexTur/pen/oNmJgQd)*

Этот код создает эффект 3D-карточки. Карточка находится внутри контейнера с классом `"transform-container"`. Сама карточка представляет собой div с классом `"transform-card"`.

```html
<div class="transform-container">
    <div class="transform-card"></div>
</div>
```
## CSS

CSS стили определяют внешний вид карточки и контейнера. Карточка имеет заданную ширину и высоту, цвет фона и тень блока. Контейнер имеет перспективу и стиль трансформации, чтобы включить эффект 3D.

```css
   .transform-container {
        perspective: 1000px;
        transform-style: preserve-3d;
    }

    .transform-card {
        border-radius: 10px;
        width: 400px;
        height: 500px;
        background-color: #fff;
        transition: transform 0.2s linear;
        box-shadow:
                0 2.8px 2.2px rgba(0, 0, 0, 0.034),
                0 6.7px 5.3px rgba(0, 0, 0, 0.048),
                0 12.5px 10px rgba(0, 0, 0, 0.06),
                0 22.3px 17.9px rgba(0, 0, 0, 0.072),
                0 41.8px 33.4px rgba(0, 0, 0, 0.086),
                0 100px 80px rgba(0, 0, 0, 0.12)
      }
```
## JS

В JavaScript-коде определены две функции: ***startRotate*** и ***stopRotate***.

Функция ***startRotate*** принимает событие `e (mousemove)` в качестве параметра и находит карточку внутри контейнера, используя метод querySelector. Затем функция вычисляет половину высоты и ширины карточки, чтобы определить точку центра карточки. Затем применяется CSS-трансформация к карточке с помощью свойства `transform`. Вращение карточки происходит вокруг осей X и Y в зависимости от положения мыши. Для этого используются свойства `offsetX`и `offsetY` с вычитанием половины высоты и ширины карточки и делением на значение `transformator`, установленное по умолчанию равным 10.

Функция ***stopRotate*** вызывается при событии `mouseout` и сбрасывает CSS-трансформацию, устанавливая значение `transform` карточки равным **"rotate(0)"**, чтобы вернуть карточку в исходное состояние.

```js
 const transformator = 10
    const cards = document.querySelectorAll('.transform-container');
    for(let i = 0; i < cards.length; i++){
        const card = cards[i];
        card.addEventListener('mousemove', startRotate)
        card.addEventListener('mouseout', stopRotate)
    }

    function startRotate(e){
        const cardItem = this.querySelector('.transform-card');
        const halfHeight = cardItem.offsetHeight / 2;
        const halfWidth = cardItem.offsetWidth / 2;
        cardItem.style.transform = 'rotateX('+-(e.offsetY-halfHeight)/transformator + 'deg) rotateY('+ (e.offsetX-halfWidth)/transformator +'deg)'
    }

    function stopRotate(){
        const cardItem = this.querySelector('.transform-card');
        cardItem.style.transform = 'rotate(0)'
    }
```

Таким образом, данный код создает эффект 3D-карточки, которая вращается в зависимости от положения мыши.
