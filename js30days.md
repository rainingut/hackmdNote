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

# day4 - console - array [alex](https://youtu.be/8JzVwrzkUrM)
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

# day7 - console
