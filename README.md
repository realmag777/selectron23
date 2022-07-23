# selectron23
Selectron23 - pure JS drop-down with API and images and description text. Its can create drop-down in usual div container, and also wrap tag select. Demo on: [codepen.io](https://codepen.io/rostislav-sofronov/pen/NWbeoYy)


Example:
```html
<div style="width: 100%; display: flex; justify-content: space-around">
    <div id="block-example" style="flex-basis: 48%;"></div>
    <div id="block-example2" style="flex-basis: 48%;"></div>
</div>
<br />
<div style="width: 100%; display: flex; justify-content: space-around;">
    <div style="flex-basis: 48%;">
        <a href="javascript: selector1.select('gbp'); void(0);">Select GBP in 1</a>&nbsp;|&nbsp;<a href="javascript: add_currency('jpy', 1); void(0);">Add JPY to 1</a>&nbsp;|&nbsp;Selected value in 1: <span id="selector1-value" style="font-weight: bold;">uah</span><br />

    </div>
    <div style="flex-basis: 48%;">
        <a href="javascript: selector2.select('gbp'); void(0);">Select GBP in 2</a>&nbsp;|&nbsp;<a href="javascript: add_currency('jpy', 2); void(0);">Add JPY to 2</a>&nbsp;|&nbsp;Selected value in 2: <span id="selector2-value" style="font-weight: bold;">uah</span><br />
    </div>
</div>

<br /><br />
<div style="width: 100%;">
    <select id="drop-down-example" name="hello_world" data-label="Select any currency" data-width="50%" data-imgpos="right" data-fusion="0">
        <option value="usd" data-img="https://pluginus.net/wp-content/uploads/2021/03/united_states_of_america.gif" data-text="United States">USD</option>
        <option value="eur" data-img="https://pluginus.net/wp-content/uploads/2021/03/european_union.gif" data-text="Euro union">EUR</option>
        <option value="gbp" data-img="https://pluginus.net/wp-content/uploads/2021/03/united_kingdom.gif" data-text="Great Britain">GBP</option>
    </select><br />
    Selected value: <span id="selector3-value" style="font-weight: bold;">-</span><br />
</div>
```


```javascript
//demo
document.getElementById('drop-down-example').addEventListener('change', function () {
    console.log('event attached to the <select>:', this.value)
});

let data1 = {
    options: [
        {
            value: 'usd',
            title: 'USD',
            text: 'United States Dollar',
            img: 'https://pluginus.net/wp-content/uploads/2021/03/united_states_of_america.gif'
        },
        {
            value: 'eur',
            title: 'EUR',
            text: 'European Euro',
            img: 'https://pluginus.net/wp-content/uploads/2021/03/european_union.gif'
        },
        {
            value: 'uah',
            title: 'UAH',
            text: 'Украинская гривна',
            img: 'https://pluginus.net/wp-content/uploads/2021/03/ukraine.gif'
        },
        {
            value: 'gbp',
            title: 'GBP',
            text: 'Great Britain pound',
            img: 'https://pluginus.net/wp-content/uploads/2021/03/united_kingdom.gif'
        }
    ],
    label: 'Select currency',
    selected: 'uah',
    width: '100%',
    imgpos: 'right',
    //name: 'my_value', //hidden input name
    fusion: false, //use if wrap <select> to fuse titles by keys with options description here
    max_open_height: 200, //max height (px) of opened drop-down when vertical scroll appears
};

var selector1 = new Selectron23(document.querySelector('#block-example'), data1);

let data2 = Object.assign({}, data1);
data2.imgpos = 'left';
delete data2.max_open_height;
var selector2 = new Selectron23(document.querySelector('#block-example2'), data2);

var selector3 = new Selectron23(document.querySelector('#drop-down-example'), {});


//demo
selector1.onSelect = function () {
    console.log('selector1', this.value);
    document.getElementById('selector1-value').innerText = this.value;
};

selector2.onSelect = function () {
    console.log('selector2', this.value);
    document.getElementById('selector2-value').innerText = this.value;
};

selector3.onSelect = function () {
    console.log('selector3', this.value);
    document.getElementById('selector3-value').innerText = this.value;
};

function add_currency(value, num = 1) {

    let selector = null;
    if (parseInt(num) === 1) {
        selector = selector1;
    } else {
        selector = selector2;
    }

    if (selector.append({
        value: value,
        title: 'JPY',
        text: 'Japan Yen',
        img: 'https://pluginus.net/wp-content/uploads/2021/03/japan.gif'
    })) {
        selector.select(value);
    } else {
        alert('JPY already in!');
}
}

```
