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

# day14 - console reference and copy [alex](https://youtu.be/sxe-oahUARI?t=705)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - console - Reference N copy" src="https://codepen.io/rainingut/embed/preview/XWKaKqQ?height=265&theme-id=light&default-tab=js" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/XWKaKqQ'>js30 - console - Reference N copy</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 字串 | 數值 | 布林
  ```javascript
  let g = 'A'
  let h = 'A'
  let i = 'A'
  h="B",i="C",g+=h,g+=i
  console.log(g,h,i)//ABC B C
  ```
  |記憶體  |  值   | 變數名  |
  |-------|-------|-------- |
  |  0x1  | "A"   |   -     |
  |  0x2  | 0x8   |   g     |
  |  0x3  | 0x5   |   h     |
  |  0x4  | 0x6   |   i     |
  |  0x5  | "B"   |   -     |
  |  0x6  | "C"   |   -     |
  |  0x7  | "AB"  |   -     |
  |  0x8  | "ABC" |   -     |
  > 示意圖：這是最後的結果，不知道A甚麼時候會被記憶體釋放..
* 陣列 - reference
  ```javascript
  const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
  let players2 = players;       // 複製陣列 '沒有真正複製'
  players2[0] = `alex`          // 更新陣列
  console.log(players,players2) // 兩個都被更新
  ```
  | 記憶體 |  值   | 變數名   |
  |-------|-------|--------  |
  |  0x1  | [...] |   -      |
  |  0x2  | 0x1   | players  | 
  |  0x3  | 0x1   | players2 |
  > 示意圖：players2 是用0x1裡面的值變更，所以players的值(0x1)自然會是一樣的..  
      為什麼兩個陣列都被更新？因為這不是「複製」，他們**對應到的是同一個陣列**

* 陣列複製的三種方法
  * ``.slice()``
  * ``[].cnocat()``
  * ES6解構``[...]``
  ```javascript
  const players = ['Wes', 'Sarah', 'Ryan', 'Poppy'];
  let players3 = players.slice()
  let players4 = [].concat(players)
  let players5 = [...players]
  ```
  | 記憶體 |  值     | 變數名   |
  |-------|-------  |--------  |
  |  0x1  | [...p1] |   -      |
  |  0x2  | 0x1     | players  | 
  |  0x3  | [...p2] |   -      |    
  |  0x4  | 0x3     | players3 |    
  * 不過下面這種,還是會修改到值
  ```javascript
  function createObj(name){
    return {name};
  }
  let p1 = createObj('alex')
  let p2 = createObj('sara')
  let p3 = createObj('mary')
  let p4 = createObj('john')
  let f1 = [p1,p2,p3,p4]
  let f2 = f1.slice()
  ```
  
  |記憶體  |  值           | 變數名  |
  |-------|---------------|-------- |
  |  0x1  | {alex}        |   -     |
  |  0x2  | 0x1           |   p1    |
  |  0x3  | {sara}        |   -     |
  |  0x4  | 0x3           |   p2    |
  |  0x5  | {mary}        |   -     |
  |  0x6  | 0x5           |   p3    |
  |  0x7  | {john}        |   -     |
  |  0x8  | 0x7           |   p4    |
  |  0x9  | [p1,p2,p3,p4] |   -     |
  |  0x10 | 0x9           |   f1    |
  |  0x11 | [p1,p2,p3,p4] |   -     |
  |  0x12 | 0x11          |   f2    |
  >記憶體的東西不可變，但**記憶體內的「物件內容」可以更動**  
  >f2[0].name  改的是 0x1 的內容，也就是說 0x1, 0x2, 0x9, 0x10, 0x11, 0x12 都會被變更
* 物件也是相似的觀念
  ```javascript
  const person = {
    name: 'WesBos',
    age: 80,
    say: function(){console.log('hi')}
  };

  let person2 = JSON.parse(JSON.stringify(person))
  ```
  > ⚠注意：使用``JSON``，function會被忽略，故沒有 ❌person2.say()
  
* 要如何複製function？ 
  用 ``call`` | ``apply`` | 閉包
  * call | apply
  ```javascript
  let fn1 = function(){return console.log('bad guy')}
  let fn2 = function(){
    fn1.apply(this,arguments)
  }
  ```
  * function clone
  ```javascript
  Function.prototype.clone= function(){
    var fct = this;
    var clone = function(){
      return fct.apply(this,arguments)
    }
    // clone.prototype = fct.prototype
    // for (property in fct){
    //   if( fct.hasOwnProperty(property) && property!=="prototype"){
    //     clone[property] = fct[property]
    //   }
    // }
    return clone
  }
  
  let fn3 = fn1.clone();
  ```
  > 上面的註解``//``拿掉可以clone得更完整，不過目前這樣就可以複製function了

---  

# day15 - localStorage - to do list[alex](https://youtu.be/gWpBTV7ihE4?t=1388)
[相關文章](https://ithelp.ithome.com.tw/articles/10232254)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - localStorage - to do list" src="https://codepen.io/rainingut/embed/KKMXQJg?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/KKMXQJg'>js30 - localStorage - to do list</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* Local storage 大小約5-10M
  * 本機端儲存庫，格式key : value
  * 只能記憶單純資料類型數值字串等
  * 關掉瀏覽器後不會消失，只能手動清除

* cookie 大小約4kb
  * 運用例如驗證 | 登入 | 購物車 等
  * server處理完資料不儲存我們所做的紀錄，是由cookie紀錄  
    下次造訪網頁時，cookie自動發送給server端

* Session storage
  * ``session``是server端儲存庫；  
    ``session storage``是本機端的儲存庫
  * 搭配cookie使用
  * 生命周期較短，關掉瀏覽器時，資料就會被清空

--- 

# day16 - mousemove N offset [alex](https://youtu.be/fa9Lk2KnARY?t=1000)
https://ithelp.ithome.com.tw/articles/10232269
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - mousemove N offset" src="https://codepen.io/rainingut/embed/pobLwwv?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/pobLwwv'>js30 - mousemove N offset</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``<h1 contenteditable></h1>``  
  ``contenteditable``可編輯，就像input:text
* Event 的屬性：
  * offsetX：滑鼠到外層容器的距離。
  * offsetY：滑鼠到外層容器的距離。
* Element 的屬性：
  * offsetWidth ：該 element 的寬。
  * offsetHeight：該 element 的高。
  * offsetLeft：該 element 到 offsetParent 的距離。
  * offsetTop ：該 element 到 offsetParent 的距離。
```javascript
let x = Math.floor((offsetX / this.offsetWidth) * length * 2 - length);
//(offsetX / this.offsetWidth) ==> 0~1
//(offsetX / this.offsetWidth) * length ==> 0~100  (length設定值設為100)
//(offsetX / this.offsetWidth) * length * 2 ==> 0~200
//(offsetX / this.offsetWidth) * length * 2 - length ==> -100~100
```

---

# day17 - sort N RegExp [alex](https://youtu.be/_fG7bQTSQ6M?t=943)
https://ithelp.ithome.com.tw/articles/10232358
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - sort" src="https://codepen.io/rainingut/embed/ExyEbKy?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/ExyEbKy'>js30 - sort</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 正規表示法``/^(a |an |the )/i``  
  (a空白開頭 或 an空白開頭 或 the空白開頭 不分大小寫)
* ES6解構(複製陣列)``[...bands]``
* 大小排序
  ``
  [...bands].sort((a,b)=>   strip(a) > strip(b) ? 1 : -1 );
  ``
* 渲染到畫面上
  ```javascript
  document.getElementById("bands").innerHTML = sortBands
    .map(band=>`<li>${band}</li>`)//map跟forEach很像.但是新的陣列
    .join("")
  ```

---

# day18 - video total time [alex](https://youtu.be/fOZGTOTKHXs?t=1710)
[loupe](http://latentflip.com/loupe/)
https://ithelp.ithome.com.tw/articles/10232374
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - hor:min:sec" src="https://codepen.io/rainingut/embed/WNxzPvZ?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/WNxzPvZ'>js30 - hor:min:sec</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``querySelectorAll`` ==> 「NodeList」「arraylike」是一個「類似陣列」的清單  
  可以用的只有「length」「forEach」。
* 可以使用四種方法將querySelectorAll轉為陣列，使用.map()
  * ``Array.from(li).map(item => item)``
  * ``[...li].map(item => item)``
  * ``[].map.apply(li, [item => item])``
  * ``[].map.call(li, item => item)``
* 案例中**加總**所有分秒
  ```javascript
  let liSecs = [...liTime]                
   .map(item => item.dataset.time)       
   .map(time => {                        
     let [min, sec] = time.split(":")                
     return min * 60 + sec *1            
  })
   .reduce((prev,next) => prev + next, 0)
  ```
* 拆分時:分:秒
  ```javascript
  let hor = Math.floor( liSecs / 3600 )
  let min = Math.floor((liSecs % 3600 ) / 60)
  let sec = liSecs % 60
  ```

--- 

# day19 - webcam [alex](https://youtu.be/1oOxMR_LPb0?t=340)
https://ithelp.ithome.com.tw/articles/10232455
<iframe height="265" style="width: 100%;" scrolling="no" title="js30  - webcam" src="https://codepen.io/rainingut/embed/preview/rNLdgGR?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/rNLdgGR'>js30  - webcam</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* 事件聆聽``canplay``
* 設定鏡頭播放
  * ``navigator.mediaDevices``：可用來串聯與麥克風、攝影機或共享螢幕的連結。
  * ``getUserMedia()``：是否允許開啟連結至其設備（只有兩個``vedio``跟``audio``）。
  * 上方會返回**promise物件**，所以要用``.then()``返回``MediaStream物件``
  * 處理vedio來源：``video.srcObject = localMediaStream``
  * 須考量到其他瀏覽器是否能正常播放，故需要``try``與``catch``
* canvas渲染 (setInterval)
  ```javascript
  const canvas = document.querySelector('.photo');
  const ctx = canvas.getContext('2d');
  ```
  * ``ctx.drawImage(來源,x1,y1,寬,高)``：  
    將圖像，畫布或視頻繪製到畫布上。
  * ``ctx.getImageData(x1,y1,寬,高)``：  
    (複製)取出相片每個像素rgba，且會返回一個ImageData物件。
  * ``ctx.putImageData(imageData,x,y)``:  
    與``getImageData``👆是一組的  
    把某區域的像素值呈現在指定的位址上
* canvas截圖
  ```javascript
  function takePhoto(){
      const data = canvas.toDataURL('image/jpeg');
      const link = document.createElement('a')
      link.href  = data
      link.setAttribute('download','handsome')
      link.innerHTML = `<img src="${data}" alt="mememe">`
      strip.insertBefore(link,strip.firstChild)
   }
  ```
  * ``canvas.toDataURL(type, encoderOptions)``:  
    這個語法可以把圖片轉成 base64，回傳含有圖像和參數設置特定格式的 data URIs (預設 PNG).，回傳的圖像解析度為 96 dpi。
* canvas濾鏡效果  
  以下0,1,2,3分別代表red, green, blue, alpha色板。
  * 紅色板
    ```javascript
    function redEffect(pixels){
      for(let i=0;i< pixels.data.length;i+=4){
        pixels.data[i + 0] = pixels.data[i + 0] + 200 //RED
        pixels.data[i + 1] = pixels.data[i + 1] -  50 //Green
        pixels.data[i + 2] = pixels.data[i + 2] + 0.5 //Blue
      }
      return pixels
    }
    ```
  * 三色板錯位
    ```javascript
    function rgbSplit(pixels){//把目標色板放到別的色板
      for(let i=0;i< pixels.data.length;i+=4){
        pixels.data[i - 150] = pixels.data[i + 0] + 200 //RED
        pixels.data[i + 500] = pixels.data[i + 1] -  50 //Green
        pixels.data[i - 550] = pixels.data[i + 2] + 0.5 //Blue
      }
      return pixels
    }
    ```
  * 綠背景去背
    ```javascript
    function greenScreen(pixels){
      const levels = {}
      document.querySelectorAll('.rgb input').forEach(input => {
        levels[input.name] = input.value
      })
      for(let i=0;i<pixels.data.length;i+=4){
        red = pixels.data[i+0];
        gre = pixels.data[i+1];
        blu = pixels.data[i+2];
        alp = pixels.data[i+3];
        if(
          red >= levels.rmin &&
          gre >= levels.gmin &&
          blu >= levels.bmin &&
          red <= levels.rmax &&
          gre <= levels.gmax &&
          blu <= levels.bmax 
        ){
          pixels.data[i+3] =0; //get rid of green 
        }
      }
      return pixels
    }
    ```

--- 

# day20 - speak to text [alex](https://youtu.be/TUgz-m-EMKg?t=588)
https://ithelp.ithome.com.tw/articles/10232494
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - speech" src="https://codepen.io/rainingut/embed/preview/GRqdpEd?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/GRqdpEd'>js30 - speech</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* Web Speech API：
  ```javascript
  //兼容性 chorom | firefox
  window.SpeechRecognition = window.SpeechRecognition || window.webkitSpeechRecognition;
  
  //建立一個speechRecognition物件
  const recognition = new SpeechRecognition();
  ```
  * ``Speech Synthesis``，文字轉語音
  * [``Speech Recognition``](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognitionResult)，語音轉文字
* Speech Recognition
  ```javascript
  recognition.interimResults = true;
  ```
  * [``interimResults``](https://developer.mozilla.org/en-US/docs/Web/API/SpeechRecognition/interimResults)是否要連續觸發  
    ``true``一直判斷聲音，一個個字會打出來；  
    ``false``預設,講完才判斷，且會一次打出來整句
  * ``.lang``判斷語言
    ```javascript
    recognition.lang = 'en-US';
    // recognition.lang = 'zh-TW';
    ```
  * 獲取語音辨識文字
    ```javascript
     recognition.addEventListener('result', e => {
      const transcript = Array.from(e.results)
        .map(result => result[0])
        .map(result => result.transcript)
        .join('');
    });
    ```
  * 可將指定文字做變化🦄
    ```javascript
    const unicornScript = transcript.replace(/unicorn |uniqlo /gi, '🦄'); 
    ```
  * [``textContent``](https://codertw.com/%E7%A8%8B%E5%BC%8F%E8%AA%9E%E8%A8%80/535058/#outline__2)：設定或是獲取某個元素內所有文字內容  
    ```javascript
    p.textContent = unicornScript  
    ```
  * ``.isFinal``當偵測語音辨識已經結束，就渲染到畫面上
    ```javascript
    if (e.results[0].isFinal) {
      p = document.createElement('p');
      words.appendChild(p);
    }
    ```
  * ``.start()``啟動語音辨識
    ```javascript
    recognition.start();
    ```


---

# day21 - geolocation [alex](https://youtu.be/Sm-HY8VyaH4?t=479)
https://ithelp.ithome.com.tw/articles/10232562
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - geolocation" src="https://codepen.io/rainingut/embed/preview/pobVjXg?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/pobVjXg'>js30 - geolocation</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``Geolocation API``：取得目前位置的經緯度、方向、速度等
  * ``navigator.geolocation.getCurrentPosition()``  
    只會觸發一次
  * ``navigator.geolocation.watchPosition()``  
    一直監看著移動的位置，像setInterval
  * ``navigator.geolocation.clearWatch()``   
    這個函式是用來取消，像clearInterval ``.watchPosition()``
* 屬性：
  * ``coords.heading``：北方為0度順時針計算
  * ``coords.speed``：目前的速度

---

# day22 - along link [alex](https://youtu.be/ttqfJsIxwJk?t=463)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - along link" src="https://codepen.io/rainingut/embed/xxOjZJa?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/xxOjZJa'>js30 - along link</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* [``getBoundingClientRect()``](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/getBoundingClientRect)相對於視窗的座標  
  包含了x/y/width/height/top/right/bottom/left 等屬性。  
  捆動卷軸會產生不一樣的座標位置，加上卷軸滾動多少的位置。
  * ``let top = `${rect.top  + window.scrollY}px` ``


--- 

# day23 - text to speech[alex](https://youtu.be/l4OZUzdCMso?t=500)
[解析1](https://ithelp.ithome.com.tw/articles/10232664) | [解析2](https://ithelp.ithome.com.tw/articles/10196799)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - text 2speech" src="https://codepen.io/rainingut/embed/qBNYNEN?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/qBNYNEN'>js30 - text 2speech</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>

* ``SpeechSynthesisUtterance``  
  Web Speech API 中代表一發音的需求，包含語言、音調、聲音、速率等資訊。
  * 屬性：
    * ``.lang``語言
    * ``.pitch``音調
    * ``.rate``速度
    * ``.text``發音文字
    * ``.voice``聲音
    * ``.volume``音量
  * 事件：
    * ``.onstart``開始發音觸發此事件
    * ``.onend``完成整句發音觸發此事件
    * ``.onboundary``單字片語間停頓觸發此事件
    * ``.onpause``發音暫停時觸發此事件
    * ``.onresume``被繼續播放時觸發此事件
* [``speechSynthesis``](https://developer.mozilla.org/zh-CN/docs/Web/API/SpeechSynthesis)  
  取得可使用的語音合成資訊，並播放或暫停發音等相關功能。
  * 事件(唯一)－``voiceschaged``
  * 方法：
    * ``.getVoices()``取得一陣列，包含目前所有``SpeechSynthesisVoice``物件裡所有發音資訊
    * ``.speak()``將一段發音加入發音庫，當前面的發音皆播放完成後，就會播放此發音。
    * ``.cancel()``移除所有的發音資訊。
    * ``.pause()``將 ``SpeechSynthesis`` 物件改為暫停的狀態。
    * ``.resume()``取消 ``SpeechSynthesis ``物件的暫停狀態。

---

# day24 - sticky nav [alex](https://youtu.be/GXePjBdEr6c?t=669)
[解析1](https://ithelp.ithome.com.tw/articles/10245289) | [解析2](https://ithelp.ithome.com.tw/articles/10196913)
<iframe height="265" style="width: 100%;" scrolling="no" title="js30 - sticky nav" src="https://codepen.io/rainingut/embed/GRqdjbp?height=265&theme-id=dark&default-tab=js,result" frameborder="no" loading="lazy" allowtransparency="true" allowfullscreen="true">
  See the Pen <a href='https://codepen.io/rainingut/pen/GRqdjbp'>js30 - sticky nav</a> by Rainy
  (<a href='https://codepen.io/rainingut'>@rainingut</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>


---

# day25 - addEventListener [alex](https://youtu.be/wfTR8GJu05Q?t=478)
[codepen](https://codepen.io/rainingut/pen/abZGpjJ) | [解析](https://ithelp.ithome.com.tw/articles/10197036) | [alex codepen](https://codepen.io/achen224/pen/QWWojpJ)
* addEventListener(參數1,參數2,參數3)
  * 參數1：監聽事件名稱字串，``如click``, ``change``等。
  * 參數2：監聽事件發生時，負責接收事件物件的物件，通常為函式(function)。
  * 參數3：選填，  
    預設``{ capture:false, once:false, passive:false}``
    * ``capture``捕獲
    * ``once``只監聽一次
    * ``passive``無法使用``e.preventDefault()``  
      就是去除DOM原有的功能
    * 如果只給一個值「false」是表示「capture:false」

* 案例一``.one>.two>.three``  
  JS處理事件的兩種模式
  1. capture(捕獲)模式 ：從外層進去  
    ``.one👉.two👉.three``
  2. bubbling(氣泡)模式：從裡層出去  
    ``.one👈.two👈.three``
    如果點了最裡面的``.three``，``.two .one``也會被觸發  
  * 防止capture往下 | 防止bubbling往上，可使用``e.stopPropagation()``
* 案例二
  ```xml
  <ul>
    <li><a href="#">hello1</a></li>
    <li><a href="#">hello2</a></li>
    <li><a href="#">hello3</a></li>
  </ul>
  ```
  * binding綁定，就是我們平常針對單一物件做事件聆聽、事件處理。
      ```javascript
      let as = document.querySelectorAll('ul a')
      as.forEach(a=>a.addEventListener('click',asHandler))
      function asHandler(e){
        e.preventDefault();
      }
      ```
  * delegate委派，針對父層做事件聆聽，再對其子層做事件處理。
    ```javascript
    let ul = document.querySelector('ul')
    ul.addEventListener('click',ulhandler)
    function ulhandler(e){
      // console.log(e.composedPath())//按下去時，JS會捕獲那些物件
      // console.log(e.target,e.currentTarget)
      if(e.target.nodeName ==='A'){
        e.preventDefault();
        console.log('Delegate: BINGO')
      }
    }
    ```
    > 注意：找``nodeName``要用全大寫  
    
    | 點擊對象 | target | currentTarget |
    |---------|---------|---------------|
    |    ul   |    ul   |       ul      |
    |    li   |    li   |       ul      |
    |     a   |     a   |       ul      |
    
---

# day26 - [alex](https://youtu.be/ndcl4hiyhQY?t=332)

---

# day27 - [alex](https://youtu.be/Opw1XH2eGb4?t=523)

---

# day28 - [alex](https://youtu.be/BOoebERng18)

---

# day29  - [alex](https://youtu.be/ucqq20gVBic)

---

# day30 - [alex](https://youtu.be/ojgYzPffW0E?t=255)
