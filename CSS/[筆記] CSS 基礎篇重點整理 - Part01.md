## [筆記] CSS 基礎篇重點整理 - Part01

### CSS ( Cascading Stylesheets )

定義 : 給 html element 套上自定義的樣式，美化頁面。

------

#### CSS Selectors 

CSS 套用樣式的方法，基本有三種，分別是 Tag selector、`class`、`id`。

```css
/* Tag selector */
p {
    color: red; // 套用到所有 p elements，使其字體顏色為紅色。
}

/* class */
.myClass {
    color: yellow; // 套用到所有有加 class="myClass" 的 elements，使其字體顏色為黃色。
}

/* ID */
#myID {
    color: blue; // 套用到所有有加 id="myID" 的 elements，使其字體顏色為藍色。
}
```

注意 : 

1. 同一個 elements 可以有多個 Class。 ex. `<p class="class1 class2"> 我套用了兩個 class </p>`
2. 優先順序 : ID > Class > Tag Selector，當 element 有重複套用樣式時，以優先順序高的樣式為優先。
3. ID 和 Class 的差異 ? Class 是可以被重複使用，ID 只能使用一次。

基本原則 : 

* 請不要為每個 element 都設定單獨的樣式，善用 class 組合。

* 請不要濫用 id，id 僅用於設置一個元素的樣式。

----

#### 常用的 CSS

* 字的樣式

```css
.font-style {
    
    /* 設定字型，中間有空格以雙引號表示，建議使用兩三個字型就好。*/
    font-family: "Courier New", sans-serif; 
    /* 設定字的大小 */
    font-size: 16px;
    /* 設定字的粗細，預設為 normal，也可以用 100~900 表示*/
    font-weight: blod | 700;
    /* 設定字的位置，置左、置中或置右 */
    text-align: left | center | right;
    /* 設定字的顏色 */
    color: red;
}
```

* BoxModel

```css 
.box-model{
    
    /* 高度、最小高度、最大高度 */
    height: 100px;
    min-height: 50px;
    max-height: 300px;
    
    /* 寬度、最小寬度、最大寬度 */
    width: 100px;
    min-width: 50px;
    max-width: 300px;
    
    /* 與邊框的距離，可以拆分為 padding-left、padding-right、padding-top、padding-bottom，
       設定順序:上、右、下、左 (clockwise rotation) 或 上下、左右 */
    padding: 2px 10px 2px 10px | 2px 10px;
    
    /* 邊框設定，預設為 medium none color，設定值:寬度、樣式、顏色*/
    border: 1px solid black;
    /* 邊框圓角設定，可以以百分比為單位 */
    border-radius: 5px;
    
    /* 邊框與其他物件的距離，可以拆分為 margin-left、margin-right、margin-top、margin-bottom，
       設定順序:上、右、下、左 (clockwise rotation) 或 上下、左右 */
    margin: 2px 10px 2px 10px | 2px 10px;
    
    /* 設定當 content 超出父元素的區域的顯示方式 */
    overflow: hidden | scroll | visible;
    
    /* 設定 element 是否被隱藏，注意只是看不到該 element */
    visibility: hidden | visible;
    
    /* 設定 BoxModel 樣式 */
    box-sizing: content-box | border-box;
}
```

* position

```css
.position {
    
    position: static | relative | absolute | fixed;
    /* 搭配 position 使用，決定 element 的前後順序，數字越大越前面 */
    z-index: ±2147483647;
    
    /* block、inline 為預設，看 element tag */
    display: block | inline | inline-block;
    
    /* 讓 elemnt 的位置移到最左邊或最右邊 */
    float: left | right;
    /* 清除 element 左邊、右邊、兩側的 flaot element，預設為 none 不清除*/
    clear: left | right | both | none;
   
}
```

------

#### CSS 其他文章

* [[筆記]CSS Box Model 篇重點整理 - Part02](C:\Users\jamiesu\Documents\我的文件\Notes\css\[筆記] CSS Box Model 篇重點整理 - Part02)
* [[筆記]CSS Element Position 篇重點整理 - Part03](C:\Users\jamiesu\Documents\我的文件\Notes\css\[筆記]CSS Element Position 篇重點整理 - Part03)
