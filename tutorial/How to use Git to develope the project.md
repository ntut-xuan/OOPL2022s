# 要怎麼使用 Git 來開發專案

\# 科普 

\# 分享性質不負責知識正確性



## 為什麼我們會需要分支

### 簡介

分支可以用來從當前的版本支線來分支，分支的意義在於「最終都會回到原分支」。

舉個簡單的例子，你（Alice）與另一個好夥伴（Bob）一起開發一個遊戲，你們的專案是從零開始的，目前專案有一個 `main` 分支。



### 舉例

你與 Bob 打好商量，你負責製作遊戲的初始畫面，而 Bob 負責製作遊戲的結束畫面，你們各自從了只有潔淨版框架的節點上開始分支。
由於你負責製作遊戲的初始畫面，所以你的分支叫做 `complete-start-up`，而 Bob 的分支叫做 `complete-end`。



接下來，你可以無憂無慮的在你的分支上做任何的事情，無論是因為自己的習慣，一點小修改就 commit ，或者決定把所有功能完成之後一次 commit，或者在推到 Github 上之後發現自己耍笨搞砸了一些東西，所以加了額外的 commit 來修補自己耍笨搞砸的東西，你在這條分支上的工作都不會影響 Bob，而這個分支的最終目的是當你完成了初始畫面的呈現，這個分支就能夠再併回去主分支。



而 Bob 也是同樣的概念，無論在 `complete-end` 如何搞砸，都不會影響到 `complete-start-up` 的分支，若覺得自己想要砍掉重練，甚至可以把分支砍掉再重分支一個新的分支（同樣的概念你也可以用 `reset --hard` 去做，但很危險），而這個分支的最終目的是完成結束畫面的呈現，然後併進去主分支。



![image-20230302035225589](https://i.imgur.com/DecJyxQ.png)



分支的存在意義就在於你們可以隨時從某個版本上分支並進行開發，這樣的好處在於，只要你們的工作是獨立的，就可以利用 merge 來併入專案部分的程式碼，且不會打擾到共同開發的人，但切記不要亂 commit 到別人的分支上，否則可能會打輸進醫院打贏進法院。



### 結論

分支存在的意義在於可以讓許多的專案維護者獨立工作，在任意版本節點上切出分支，並在該分支上完成應該做的事情。



## 為什麼我們會需要 Pull Request

### 簡介

你，Alice，花了許久時間之後終於完成了初始畫面的呈現，接下來你想要將 `complete-start-up` 這個分支併入 `main` 上。

由於 `main` 是共用的分支，大家都在維護這個分支，要從原本只有你維護的分支併入大家一起維護的分支，就得要通知大家說「我要併入 `main` 囉」。

這時候我們就會使用 Pull Request 來做「告知大家併入分支」這件事情。



### 比較生活化的舉例

接下來的舉例會用一個比較生活化的方式來舉例：



你（Alice）跟 Bob 住在兩房一廳的租屋處，你是一個比較注意生活的女生，由於家裡客廳的地毯已經髒亂不堪，你想要把家裡的地毯換成新的。

但地毯是公共設施，也就是你與 Bob 會共用的，你沒辦法就單純覺得想丟就丟，這件事情還得跟 Bob 商量，所以：

- 你提議把地毯換成新的
- 你告訴了 Bob 你要把地毯換成新的
- Bob 表示同意（approved）
- 你可以換地毯了，然後把地毯換成新的，租屋處的客廳就有新的地毯了。



把這個奇怪的例子轉換成 Git 的分支，就會像這樣。

<img src="https://i.imgur.com/bjV8lbz.png" alt="image-20230302040309824" style="zoom:67%;" />

你是 Alice，擁有了 `change-the-carpet` 這個分支，並且完成了地毯換新的動作。

![image-20230302040135606](https://i.imgur.com/D77s0Pr.png)

注意下面這張圖的分支是 `change-the-carpet` 的 `README.md`

<img src="https://i.imgur.com/MrYWcJt.png" alt="image-20230302040421840" style="zoom:67%;" />

你跟 Bob 說你要換地毯，所以 main 分支的地毯會換新的，於是你開了一個 Pull Request，並將 reviewer 設成 Bob。

<img src="https://i.imgur.com/bPpWPOC.png" alt="image-20230302040722772" style="zoom: 80%;" />

![image-20230302040844199](https://i.imgur.com/qhfgOf6.png)

接下來如果 Bob 同意了這個 PR，地毯就可以被併入 `main`，此時 `main` 就會有新的地毯了。

那麼如果 Bob 不喜歡這個地毯，它也可以把 PR 給 close 掉，代表拒絕把 `main` 的地板更新，這個分支就變得無用了（或者可以修修補補再 PR 一次）。

注意下面這張圖的分支是 `main` 的 `README.md`。

![image-20230302040916644](https://i.imgur.com/HG232bZ.png)

此時 `change-the-carpet` 分支就會結束它的使命，你就可以把 `change-the-carpet` 分支刪除了。

併入 main 分支後的節點圖就會長得像下面這張圖。

![image-20230302041032838](https://i.imgur.com/s5mjVIO.png)



### 結論

所以這就像是告訴你的專案開發夥伴，你完成了遊戲的某一個部分，然後你準備併入到你們共用的分支（主支線）上，只要你的專案開發夥伴同意，這個分支就能併入主支線，這樣也可以讓專案開發夥伴知道你在這個分支做了些什麼事情，還有哪些事情需要修改，或者這個分支它覺得看起來是不是能夠併入分支內。

如果我們沒有這樣做的話，你會隨著開發，發現 Alice 可能把你家的牆壁從白色漆成死亡芭比粉，把地墊換成了紙板，把門拆了就直接奪門而出（臨走前還嗆你門都沒有！），這些更動都沒有經過你的同意，你們的共用空間就變成 Alice 想幹嘛就幹嘛了（顯然日常生活中的同居不能這樣，那麼開發專案也不能這樣，需要好好溝通更動了哪些東西。）



## 結論

有了這樣的開發方式，可以有助於在開發時保持與其他夥伴的共識，並且可以互相監督彼此的軟體品質是否是好的。

且這樣的開發方式不僅僅是多人才能，單人也可以（只是會變成很像在自言自語），保持這樣的好習慣就能讓團隊的開發更加順暢。



下圖演示了如果單人開發，節點圖會長的樣子，也就是將支線新增功能，併入主支線之後再從主支線分支，然後新增功能後再併入主支線。

![image-20230302041850213](https://i.imgur.com/pYzMAFT.png)

以上是我撰寫的《如何使用 Git 開發專案》，若有興趣也可以更深入探討，非常歡迎！