# 00 Get started

`framework` : `library` + `rules`.

<img src="assets/Screenshot 2020-09-21 at 16.55.44.png" alt="Screenshot 2020-09-21 at 16.55.44" style="zoom:67%;" />

## Deux façon d'appréhender `Vue`

1. widget : une partie d'une application qui n'est pas gérée par `Vue`
2. Single Page Application : `Vue` gère la totalité de l'application



## `JS` vs `Vue`

### js style

```html
<!DOCTYPE html>
<html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Document</title>
    </head>
    <body>
        <h3>Goal</h3>
        <input id="goal" type="text" placeholder="finish your goal !" />
        <br />
        <p><button>Add Goal</button></p>
        <ul id="goals"></ul>
        <script src="./app.js"></script>
    </body>
</html>
```

```js
const buttonEl = document.querySelector('button')
const inputEl = document.querySelector('input')
const ulEl = document.querySelector('ul')

buttonEl.addEventListener('click', () => {
    const enterredValue = inputEl.value
    const liEl = document.createElement('li')
    liEl.textContent = enterredValue
    ulEl.appendChild(liEl)

    inputEl.value = ''
})
```

### Vue style

