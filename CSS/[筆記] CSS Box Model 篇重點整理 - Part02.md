## [筆記] CSS Box Model 篇重點整理 - Part02

#### Box Model

定義 : Box Model 盒子模型，所有的 Html element 都可以被視為一個盒子，然後可以在 CSS 下針對盒子有的屬性做調整，來改變其外觀。 

模型架構圖 : 

![box-model](圖片\Box-Model.png)

- **Content** - 實際上顯示 element 內的內容的地方，像是文字或圖片。

- **Padding** - content 到邊框間空白的區塊。

- **Border** - 包圍 content 和 padding 的邊框。

- **Margin** - 邊框以外到其他 element 間空白的區塊。

  

---



#### [使用 margin + auto 置中](https://stackblitz.com/edit/margin-auto-to-center?file=src/app/app.component.css)

  ```css
/* select <div> element with class="banner" */
div.banner {
    width: 400px;
    margin: 0 auto;
}
  ```

注意:

* `<div>` 預設的寬度為全寬，所以需要設定寬度，才能始置中生效。

#### Margin Collapse

垂直方向的 margin ( top、buttom ) 會產生組合效果，水平方向不會，如以下範例。

```CSS
#box-one{
	margin: 30px;
}

#box-two{
	margin: 20px;
}
```

![margin-collapse](圖片\Margin-collapse.png)



#### Box-sizing

控制 Box-Model 的顯示方式，預設為 content-box。

content-box : 會讓 element 實際長度和寬度 = 設定的長寬(width / height) + padding + border。

border-box : 會讓 element 實際長度和寬度 = 設定的長寬(width / height)，而 padding 和 border 的長寬包含在其中。

```css
box-sizing: content-box | border-box;
```

![box-sizing](圖片\box-sizing.png)

----



#### 常用 CSS Box Model

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

