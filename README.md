# selectron23
JS drop-down with images and description text. Its can create drop-down in usual div container, and also wrap tag select. Demo om: [codepen.io](https://codepen.io/rostislav-sofronov/pen/NWbeoYy)


Example:
```html
<div style="display: flex; justify-content: center; flex-direction: column; ">
    <div style="width: 100%; padding-bottom: 40px;">
        <div id="block-example"></div>
        <br />
        <a href="javascript: selector1.select('gbp'); void(0);">Select GBP</a>
      &nbsp;|&nbsp;<a href="javascript: add_currency('jpy'); void(0);">Add JPY</a>
      &nbsp;|&nbsp;Selected value: <span id="selector1-value">-</span><br />
    </div>

    <div style="width: 100%;">
        <select id="drop-down-example" name="hello_world">
            <option value="1">uno</option>
            <option value="2">dos</option>
            <option value="3">tres</option>
        </select><br />
        Selected value: <span id="selector2-value">-</span><br />
    </div>
</div>
```


```javascript
//demo
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
    //selected: 'uah',
    width: '90%',
    img_position: 'right',
    input: 'my_value', //hidden input name
    fusion: false//use if wrap <select> to fuse titles by keys with options description here
};

var selector1 = new Selectron23(document.querySelector('#block-example'), data1);

let data2 = Object.assign({}, data1);
delete data2.selected;
data2.img_position = 'left';
data2.label = 'Select Number';
var selector2 = new Selectron23(document.querySelector('#drop-down-example'), data2);


//demo
selector1.onSelect = function () {
    console.log('selector1', this.value);
    document.getElementById('selector1-value').innerText = this.value;
};

selector2.onSelect = function () {
    console.log('selector2', this.value);
    document.getElementById('selector2-value').innerText = this.value;
};

function add_currency(value) {
    if (selector1.append({
        value: value,
        title: 'JPY',
        text: 'Japan Yen',
        img: 'https://pluginus.net/wp-content/uploads/2021/03/japan.gif'
    })) {
        selector1.select(value);
    } else {
        alert('JPY already in!')
    }
}

```
