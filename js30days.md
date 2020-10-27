# javascript 30days
[原主](https://javascript30.com/) | [原主github](https://github.com/wesbos/JavaScript30)
# day 1 - keycode - drum [alex](https://youtu.be/f2ttaeDHzwE)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - drump" src="https://codepen.io/rainingut/embed/oNLZYNr?height=265&theme-id=dark&default-tab=html,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/oNLZYNr'>js30 - drump</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* window事件聆聽keydown ==> 觸發function，
  此function播放「audio」以及加入「style」。
* 當播放轉場結束，移除該「style」。

---

# day2 - clock [alex](https://youtu.be/O1YsB3qxO4g)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - clock" src="https://codepen.io/rainingut/embed/pobeNqQ?height=265&theme-id=dark&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/pobeNqQ'>js30 - clock</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 「;(function(){//...})()」這是甚麼？ [IIFE](https://developer.mozilla.org/zh-TW/docs/Glossary/IIFE)
    * 全名：Immediately Invoked Function Expression**立即呼叫函式表達式**
    * 這樣的寫法可以避免裡面的變數污染到 global scope。
    * 立刻轉譯該 function
* 控制時間的三種咚咚
    * setInterval　　　　　　 設定間隔，持續執行
    * setTimeout　　　　　　設定延遲，執行一次
    * requestAnimationframe 處理畫面更新的setTimeout


---

# day3 - color range (drag) [alex](https://youtu.be/fIE2Lmfbo4k)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - color" src="https://codepen.io/rainingut/embed/jOrByLo?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/jOrByLo'>js30 - color</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* CSS「:root」運用(變數)
  ```css
  :root{--base: #fb3;}
  .hl{color: var(--base)}
  ```
* document.querySelector(':root')
  === document.querySelector('html')
  === document.documentElement
* 「:root」與「setProperty」與「dataset」的運用
  ```javascript
  const inputs = document.querySelectorAll('input')
  inputs.forEach(function(input){
    input.addEventListener('change',styleHandler)
    input.addEventListener('mousemove',styleHandler)
  })
  
  function styleHandler(){
  const unit = this.dataset.sizing || ''
    document.documentElement.style.setProperty(`--${this.name}`,this.value+unit)
  }
  ```
  
---

# day4 - array - console [alex](https://youtu.be/8JzVwrzkUrM)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - console" src="https://codepen.io/rainingut/embed/zYBZwgO?height=265&theme-id=light&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/zYBZwgO'>js30 - console</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* array的功能~
1. filter－過濾（做一個新陣列）
      ```javascript
    let ans1 = inventors.filter(function(inven){
          return inven.year >= 1500 && inven.year < 1600;
    })
      ```
2. map－針對每個內容產生新的動作（做一個新陣列）
   forEach－針對每個內容產生新的動作（對原有陣列做變化）
   ```javascript
   let ans2 = inventors.map((inven)=>`${inven.first}  ${inven.last}`)
   console.table(ans2)容
   //---
   let ans2p5 = [];
   inventors.forEach((inven)=>ans2p5.push(inven.first + inven.last))
      ```
3. sort－排序（做一個新陣列）
      ```javascript
    let ans3 = inventors.sort((a,b)=>a.year - b.year);//<0 | ==0 | >0
    //-1 | 0 | 1 這樣子去排序
      ```
      ```javascript
    inventors.forEach((inven)=>{//foreach幫我做事情，但不會產生新陣列
      inven.years = inven.passed - inven.year
    })
      ```
      ```javascript
    let ans7 = people.sort((a,b)=>{
        let [afirst,alast] = a.split(', ')
        let [bfirst,blast] = b.split(', ')
        return alast[0] > blast[0] ? 1 : blast[0] > alast[0] ? -1 : 0;//[0]代表第一個字
      })
      ```
4. reduce－加總（做一個新陣列）
    ```javascript
    let ans4 = inventors.reduce((total,inven)=>{
      return total + inven.passed - inven.year
    },0)
    // 1st次 ==> 0
    // 2nd次 ==> 0 + (1955 - 1879)
    // 3rd次 ==> 0 + (1955 - 1879) + (1727 - 1643)

    //---
    
    let total =0;
    inventors.forEach((inven)=>{
      total += inven.passed - inven.year
    })
      ```
      ```javascript
    //計算重複幾次
    const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck' ];
    let ans8 = data.reduce((obj,content)=>{
        if(!obj[content])obj[content]=1
        else obj[content] += 1; 
        return obj
    },{})//這裡的「,{}」是起始值
      ```
      
---

# day5 - flex [alex](https://youtu.be/7hGFTNGommU)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - flex" src="https://codepen.io/rainingut/embed/eYzvGBL?height=265&theme-id=dark&default-tab=css,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/eYzvGBL'>js30 - flex</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* classList.toggle
* flex:1 👉 flex:3
* ``物件.addEventListener('transitionend',函式)``
    * ``e.propertyName.indexOf('flex')``
    如果沒有抓``e.propertyName``，就會變成有多少樣式執行``transition``，``transitionend``就會執行幾次
    
---

# day6 - ajax,RegExp,fetch - search [alex](https://youtu.be/_TbG2iuN9kM?t=445)
⭐👉⭐需再複習....覺得難懂...
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - list" src="https://codepen.io/rainingut/embed/xxOqYge?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/xxOqYge'>js30 - list</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ajax技術方法一：xhr
* ajax技術方法二：fetch
* [RegExp](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Guide/Regular_Expressions)正規表示法
* ``toLocaleString()``
* (待補...怎麼自己撈資料..)

---

# day7 - array - console [alex](https://youtu.be/OdNA37WSwzc?t=610)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - console" src="https://codepen.io/rainingut/embed/preview/VwjpQXv?height=265&theme-id=light&default-tab=js" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/VwjpQXv'>js30 - console</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

1. some - 只要有一筆符合條件，整體就是true
  ```javascript
  //範例: 有大於等於19歲的人嗎?
  const ans1 = people.some(p =>{
    return new Date().getUTCFullYear() - p.year >= 19;
  })
  ```
2. every - 整體符合條件才true
  ```javascript
  //範例: 有大於等於19歲的人嗎?
  const ans2 = people.every(p =>{
    return new Date().getUTCFullYear() - p.year >= 19;
  })
  ```
3. find - 會找到第一筆符合條件的資料，如果有重複的不會再繼續找
  ```javascript
  //範例: 找到id: 823423
  const ans3 = comments.find(c=>c.id===823423)
  //console看是> {text: "Super good", id: 823423}
  ```
4. findIndex - 找到他在第幾筆，也是只有找第一筆資料
  ```javascript
  //範例: 找到id: 823423
  const ans4 = comments.findIndex(c=>c.id===823423)
  //console看是 1
  ```
5. 使用slice | splice刪除
   * splice: 對原始資料做修改。它可以在特定的位置刪東西 | 加東西。
    .splice(第幾個開始, 刪掉幾個 [, 增加幾個])
    ```javascript
    const ans6p2 = comments.splice(ans4,1)
    ```
    ...解構方式複製一份做刪除(⭐不會影響原始資料)
    ```javascript
    const ans6 = [...comments].splice(ans4,1)
    ```
   * slice: 複製一份原始資料做修改。
    .slice(從第幾個開始,切到哪裡(不包含這個))
    ```javascript
    const ans5 = comments.slice(0,ans4)     //目標物件的前面資料
    const ans5p2 = comments.slice(ans4 + 1) //目標物件的後面資料
    const ans5p3 = [...ans5, ...ans5p2]     //目標物件的前面資料 + 後面資料 (不含目標物件就對了..)
    ```

* 補充 - find - 以購物車作範例
  ```javascript
  const cart = [
    { id: 1 , count: 1 },
    { id: 2 , count: 1 },
    { id: 3 , count: 1 },
    { id: 4 , count: 1 }
  ]
  ```
  ```javascript
  //用find改變指定商品數量
  const testans1 = cart.find(c=>{
    return c.id ===3
  })
  testans1.count = 5;
  ```
  ```javascript
  //用一個新變數修改 (但原始資料也會被更動..(傳值傳址))
  const newcart = [...cart];
  newcart[0].count = 3
  console.log(newcart[0],cart[0])
  ```
---
# day8 - canvas - painting [alex](https://youtu.be/3862i0RdKLU?t=409)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - canvas" src="https://codepen.io/rainingut/embed/BazWgYO?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/BazWgYO'>js30 - canvas</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``.getContext('2d')``
* strokeStyle, lineWidth, lineCap, lineJoin, beginPath(), moveTo(x,y), lineTo(x,y), stroke()
* 事件聆聽``mousedown``, ``mousemove``, ``mouseup``, ``mouseleave``, ``mouseout``
  * ``mouseleave``-離開畫布的時候(非冒泡事件)
  * ``mouseout`` - 離開畫布的時候(連續觸發的冒泡事件)
* 從大變小從小變大
  ```javascript
    if(ctx.lineWidth <=1 || ctx.lineWidth>50){
      widthDeg *=-1;
    }
    ctx.lineWidth += widthDeg
  ```

---
# day9 - console運用 [alex](https://youtu.be/sWBSxMVMbjc?t=384)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - console" src="https://codepen.io/rainingut/embed/preview/GRqWVrz?height=265&theme-id=light&default-tab=js" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/GRqWVrz'>js30 - console</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 方便開關console
  ```javascript
  let console = {
      isDev: true,
      log(...args){
        if(!this.isDev) return;
        window.console.log(...args);
      },
      warn(...args){
        if(!this.isDev) return;
        window.console.warn(...args);
      },
   //...下略
  }
  ```
* 變數
  * ``%s``字串
  * 👆可以用ES6語法替代
  * ``%f``浮點數
  * ``%d``取整數
  * ``%c``加入CSS樣式
  ```javascript
  console.log("my name is %s !!!", "Rainy");//%s字串
  console.log("I have %f dollars!!!", 3.45);//%f浮點數
  console.log("I have %d dollars!!!", 3.45);//%d取整數
  console.log(`my name is ${name} !!!`);//ES6
  console.log("%c住手!!", "font-size:35px; color:red;");//%c CSS style
  ```
* 警告``console.warn()``
* 錯誤``console.error() ``
* 偵測``console.assert(null,"顯示")``  
  (若1st數值不是true一律顯示)  
  (反之,1st數值為true則不顯示)
* ``console.table()``大量資料使用
* 計數(出現幾次)``console.count``
* 程式執行時間
  ``console.time(我是一個程式)``
  ``console.timeEnd(我是一個程式)``

---

# day10 -  multiple check [alex](https://youtu.be/tYBwiyjC_6A?t=885)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - multiple check" src="https://codepen.io/rainingut/embed/MWemgeQ?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/MWemgeQ'>js30 - multiple check</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``querySelectorAll``放入陣列中
  ```javascript
  const cbxs = Array.from(
    document.querySelectorAll('input')
  )
  ```
* 邏輯判斷
  * 目標有沒有✅
  * 有沒有第一個✅ && 有沒有按shift
  * 有第一個✅、有另一個✅  
    比大小,將這個區間全選。

--- 

# day11 - player [alex](https://youtu.be/gS4RJkcEyPo?t=625)
這裡不好意思就直接貼原著的code了...
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - player" src="https://codepen.io/rainingut/embed/qBNmWVz?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/qBNmWVz'>js30 - player</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

[my custom...](https://codepen.io/rainingut/pen/OJXmLEp)

---

# day12 - splice - secret code [alex](https://youtu.be/hY5JxUquoXM?t=269)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - secret code" src="https://codepen.io/rainingut/embed/pobPoam?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/pobPoam'>js30 - secret code</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 設定密碼
* 設定空陣列,事件聆聽keyup時push ``e.key``進去。
* 用``.splice()``切陣列判斷 
  ```javascript
  pressed.splice(-selectCode.length-1,
    pressed.length-selectCode.length)
  ```
  * ``-selectCode.length-1``從最後面開始 抓selectCode的字數(6)
  * ``pressed.length-selectCode.length``例如：
    | pressed的字 | selectCode的字 | pressed.splice後的結果 |
    | -------- | -------- | -------- |
    | ebsc     | wswooc(字數6) | ebsc     |
    | eevvggc     | wswooc(字數6) | evvggc     |
    | qwerrttyrtee     | wswooc(字數6) | tyrtee     |

--- 

# day13 - scroll [alex](https://youtu.be/PRRZlAVvJ7A?t=646)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - scroll" src="https://codepen.io/rainingut/embed/XWKRbRP?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
See the Pen <a href='https://codepen.io/rainingut/pen/XWKRbRP'>js30 - scroll</a> by Rainy
(<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 當前畫面的scrollTop  
  可用``window.scrollY``或``window.pageYOffset``取值
  ```javascript
  let scrollTop = window.scrollY;
  ```
* 當前畫面的scrollBttom  
  可用``(window.scrollY) + (window.innerHeight)``或
  ``(window.pageYOffset) + (window.innerHeight)``取值
  ```javascript
  let scrollBtm = window.innerHeight + scrollTop;
  ```
* 當前畫面的觸發位置//我自己寫上去的XD
  ```javascript
  let trggerDeg = ((scrollBtm - scrollTop) / 1.5)  + scrollTop
  ```
* 恩..覺得閉包比較難懂..(debounce)
  ```javascript
  function debounce(func, wait = 20, immediate = true) {
      var timeout;
      return function() {
        var context = this, args = arguments;
        var later = function() {
          timeout = null;
          if (!immediate) func.apply(context, args);
        };
        var callNow = immediate && !timeout;
        clearTimeout(timeout);
        timeout = setTimeout(later, wait);
        if (callNow) func.apply(context, args);
     };
  }
  ```
* lazy loading img - [codepen](https://codepen.io/rainingut/pen/zYBwvXK)

---

# day14 - console 傳值傳址