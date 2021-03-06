# 加密貨幣介紹

介紹會分成三個部分

- 比特幣和區塊鏈
- 以太坊和以太幣

同時下方也會有多個影片連結可以參考



## 比特幣和區塊鏈

區塊鏈技術起始於在2008年在中本聰的比特幣白皮書裡面首次出現，做為比特幣的底層技術，本質上就是基於密碼學的一個點對點（P2P）的分散式資料庫，相對於傳統中心化的資料庫資料都儲存在同一個地方，區塊鏈將資料分散儲存在各的地方，也就是所謂的**節點**。所以對於加密貨幣來說，區塊鏈其實就是一個分散式的帳本。



### 首先來看區塊鏈有哪些特性

- **去中心化**

  不依賴於某些額外的第三方機構，沒有任何中心管制。這種點對點分散式的架構為區塊鏈最突出的特性

- **匿名性**

  單從技術來看，各個節點身份資料不需要公開或是驗證，在交易操作上可以匿名進行，因此不會洩漏使用者的實際身份。

- **開放性**

  區塊鏈技術本身的基礎是開源的，並且任何人都可以輕易地在公開的介面平台上查詢在區塊上面任何的交易紀錄。

- **安全性**

  也就是資料的不可篡改性。只要沒有任何群體擁有超過50%的全網算力，就無法任意修改過往的交易紀錄，建立了區塊鏈本身的安全性。

- **共識性**

  在區塊鏈上每個節點得互相信任，彼此之間有共識，在這個分散式的架構中每個節點都有同樣的共識哪些才是該被放在區塊裡的交易紀錄，這個依據就是區塊鏈的共識演算法，下方會有更詳細的共識演算法說明。



### 簡單講解區塊鏈使用到的密碼學

- **雜湊函數（Hash function）**

  一種單向的數學的函式，透過此函式能把輸入的資料轉換成一串沒有意義的字符，達到把輸入的資料打亂的效果，而且此結果並沒有辦法回推輸入的資料

  ex: cat ----hash function f(x)------> a235jkjvoa09aejoivzpdle （此輸出沒有辦法回推輸入的資料為cat）

- **非對稱加密**

  使用非對稱加密的每個使用者都會有一對(兩把)鑰匙，一把為私密鑰匙(private key)可以用來加密，另一把為公開鑰匙(public key)用來解密。公開鑰匙可以被廣泛的發佈，而私密鑰匙必須被妥善地保存。其中非對稱加密的過程是單向的，並且一把密鑰加密後的資料只能用他相對應的公鑰來解開。常見的非對稱加密為 RSA, ECC (橢圓曲線)。

- **數位簽章**

  屬於一種使用橢圓曲線的非對稱加密的應用，使用者利用自己的私鑰加密（簽名），而其他人可以利用這位使用者的公鑰來驗證使用者的簽名是否為本人。



### 區塊與鍊

顧名思義是由許多區塊串成的一條練，每個區塊包含了區塊頭（Block Header）以及區塊體（Block Body）

- Block Header 包含了以下資料

  - 前一個 block 的 hash 值
  - 時間戳（Timestamp）
  - 隨機數（Nonce）
  - 當下 block 的 merkle tree root 的 hash 值

- Block Body 包含了該 block 打包好的交易紀錄

  - 交易紀錄（Transactions）

    這些在 block body 裡面的 transactions 以一種叫 merkle tree 的樹狀結構的方式儲存，可以想像 merkle tree 為一層一層的 hash 值建成的樹。有了 merkle tree 之後我們可以得出他的根（root）的 hash 值，這個值被儲存在 block header 當中，由於交易紀錄的任何變動，會導致 merkle tree root 算出的 hash 值不同，而造成 block header 的 hash 也會跟著改變，所以這說明了上了練的區塊的交易紀錄的不可篡改性。如果有人想修改某個區塊的交易紀錄，那還必須自行把後續的所有 block 都算出來並且算得比其他人都還快，成為最長的那條鏈，才能算是篡改成功，幾乎是不可能的事情。 



### 傳播機制

因為區塊鏈為點對點的網路，需要每個節點的共同協作才能保持區塊鏈的運行，那麼想要交易的人，也必須讓大家知道你想進行交易的消息。假設今天有兩個人分別是 Alice, Bob， Alice 想要給 Bob 1個 BTC，Alice 會向網路上的節點廣播他的交易訊息（transaction），廣播的內容會包括 Alice 的數位簽章，公開鑰匙，交易內容等等，給網路上的節點進行驗證，驗證通過的交易訊息會被收錄到區塊當中。



### 共識機制

前面提到區塊鏈就像帳本一樣記錄著所有的交易紀錄，那該由誰來造出區塊（記帳），記帳的人又能得到什麼好處？

- 記帳（俗稱**挖礦**）的好處

  可以獲得每筆收錄交易的手續費，以及最重要的成功出塊的人可以獲得一筆費用。以比特幣來說，2008～2012年一個區塊會有 50 顆 BTC 的獎勵，每四年減半一次，截止至目前 2020 年現在一個區塊的獎勵只剩下 6.25 顆 BTC，目的就是控制 BTC 的總量在 2100 萬顆，保持他的稀缺性，也避免通貨膨脹。

- 由誰來記帳

  這就是由這個區塊鏈的共識機制來決定，不同的幣會有不同的共識機制，比特幣的共識機制為工作量證明（Proof of Work），顧名思義，用工作量來決定誰來出塊。在這個前提下我們需要一個計算起來非常困難但是驗證結果非常容易的方法，然而 Hashcash 算法就符合這樣的場景，可以想成是一個 hash function。比特幣的計算題目為要算出的結果為前面有 n 位 0 的一個值，輸入的資料為區塊的一些資料再加上一個隨機數（Nonce），得到的結果可能會是 00101011100.....，假設題目要求為前面有 10 位 0 的答案，那麼就繼續更改隨機數，每次使用 nonce + 1，來獲得新的結果，一直試一直試，假如 nonce 試到 900 的時候，答案為 00000000001011..，此時就是算出答案了，那麼這個挖礦的人就可以向大家廣播自己包好的區塊，其他人在驗證的時候只要把它輸出的資料再加上他說他使用的隨機數就可以很容易驗證答案前面的 10 位 0。驗證通過各個節點就會把區塊接上，再繼續算下一個區塊。



### 最長鍊機制

全世界的有許多的礦工，假如有兩個人同時算出正確答案該怎麼決定？

這時候區塊鏈上就會出現分岔，兩條分岔都會有人在繼續的挖礦，時間久了，兩條鏈都變長了以後就會有算力的差別（工作量的不同），此時比較長的那條鏈會被最多人採用，因為工作量最大，代表大部分人都相信這條分岔，進而在繼續在最長鍊上挖礦。這也保證了區塊鏈的唯一性和安全性。



### 附錄

在此提供一些參考資料和影片會有更多的補充，各位有空都可以看看

李永樂老師的影片

- https://www.youtube.com/watch?v=g_fSistU3MQ
- https://www.youtube.com/watch?v=pbAVauYsqP0
- https://www.youtube.com/watch?v=e9KVmyI1eCg

老高的影片

- https://www.youtube.com/watch?v=sjx_rpay9rk
- https://www.youtube.com/watch?v=7B-1vDFuYRk





## 以太坊和以太幣

以太坊（Ethereum）是一個開源的有智能合約功能的公共區塊鏈平台，而在這條區塊鏈上的獎勵貨幣稱為以太幣（Ether），以太坊的用途超越虛擬貨幣，是去中央化應用程式的平台，能執行智慧合約。



### Ethereum

Ethereum 這條區塊鏈和比特幣的區塊鏈不一樣的地方就是在每個 block 裡面多存了一個東西叫 state tree root，那 state tree 的內容，記錄著有參與交易的所有帳號以及 data 資訊。根據 miner 收錄進來的 transactions，state tree 會改變他的狀態，直到跑完最後一個 transaction，再加入獎勵的交易紀錄，便是 state tree 的最後狀態。



在模型上，Ethereum 採用的是 account based 的模型，對比比特幣的 utxo 模型，是完全不同概念。account based 可以理解為每個人都可以擁有一個或數個帳號，這個帳號裡面就是記錄著有多少錢，這類型的帳號叫做 Externally Owned Accounts。那也有屬於智能合約的帳號，叫做 Contract Accounts，裡面也有記錄著這個帳號裡面有多少錢，並且還有可以自動執行的腳本（程式碼）。



### 智能合約 Smart Contract

智慧合約是一種事件驅動的程式，滿足某種條件後，就會自動在區塊鏈上執行，可以想像成是在區塊鏈上自動化的腳本，讓工作流程自動化。同時，智慧合約亦可以另外使用記憶體（Memory）來儲存合約所需要紀錄的資訊。例如：一個發行 ERC-20 Token 的智慧合約，便可以使用記憶體來 **紀錄各個以太坊地址所「持有 Token 數量」**，追蹤各個地址的 **ERC-20 Token Balance**



那 ERC-20 其實並不是一種技術或是一套程式，而是在 Ethereum 上的一種通訊協議，滿足此協議的 token 就可以稱之為 ERC-20 TOKEN，ex: 超多上百種的 ICO TOKEN, USDT-ERC20 等等。 其中此協議包括需要有這 6 種功能

- TotalSupply (總發行代幣量)
- BalanceOf (某個 owner的剩餘代幣量)
- Transfer (傳送多少錢到哪個帳號)
- TransferFrom (從某個帳號傳送多少錢到另一個帳號)
- approve (容許某個 spender 從 owner 錢包中不限次數地提取代幣，直到達到訂下的數量。如果此指令被更新，新的限額會取替舊的限額)
- allowance (匯報某個 spender 尚可從 owner 錢包提取的代幣數量)

由於所有 ERC-20 的代幣都可以很方便的利用 Ethereum 的生態來做交易，監測，追蹤，發行代幣的公司並不需要自己開發額外的工具或系統，所以一般來說許多人想要發行自己的代幣會選擇實作這個通訊協議來發行。



## 總結

有關於基礎加密貨幣的知識大概就介紹到這邊，感謝收看。