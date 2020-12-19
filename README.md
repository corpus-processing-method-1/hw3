# hw3: Collostructional analysis


## 作業要求

從 PTT 自行爬取文章、清理後，對文本進行 collostructional analysis (Collexeme Analysis, Distinctive Collexeme Analysis, Covarying Collexeme Analysis 三擇一)


## 繳交內容

1. 資料前處理 (資料爬取與清理、斷詞與 PoS tag): `preprocessing.R` (or `.py`)
1. Collostructional analysis: `(distinctive/covarying_)collexeme_analysis.R` (or `.py`)
    - 如果使用 Gries 的 `coll.analysis.r` 進行分析，程式碼內需包含將資料處理成 `coll.analysis.r` 所要求的輸入格式，並且在程式碼註解內記錄下自己使用的分析選項 (執行 `coll.analysis.r` 時，它要你選擇與輸入的那些資訊)
1. 分析結果
    - 請在 `README.md` (這份檔案，請刪除目前的內容) 內簡要說明：
        1. 進行了哪些分析 (Collexeme Analysis, Distinctive Collexeme Analysis, Covarying Collexeme Analysis)
        2. Construction 的定義 (i.e., 如何透過程式找出這種 construction)
        3. 分析結果檔案名稱：表格資料或 Jupyter Notebook 等，記錄分析的**數值資訊** (e.g., 至少需有 attraction 與 repulsion 最強的前十名排序與分數)。如果使用 `coll.analysis.r`，可直接使用此表格


## 小提示

1. Collostructional analysis 的提出者 Stefan Th. Gries 有提供 [collostructional analysis 的 R script](http://www.stgries.info/teaching/groningen/coll.analysis.r)，關於 collostructional analysis 的三種分析所需的資料輸入格式見 <http://www.stgries.info/teaching/groningen/index.html>。
1. 師大陳正賢老師有線上教科書示範如何 R 進行 Collexeme Analysis：<https://alvinntnu.github.io/NTNU_ENC2036_LECTURES/constructions-and-idioms.html>
1. 關於 Python 的 Distinctive Collexeme Analysis 與 Covarying Collexeme Analysis 的實作可以參考 <https://github.com/lopentu/hocor2020-GramColl> (品質不保證)
1. 目前各位遇到最大的問題可能不是 collostructional analysis 本身而是如何透過程式去找出自己想要的 construction:
    - 最簡單 (完全自行手作) 的方式是將爬回來的文章進行斷詞與 PoS tag 後，再將結果合併當成字串處理，如此便可以透過 regular expression 去找出想要的 construction。例如，將文章處理成下方的字串格式(`<詞彙>_<PoS> <詞彙>_<PoS> ...`)之後，便可透過 `把_P \S+_N[a-zA-Z]* \S+_V[a-zA-Z]*`(RegEx) 去抓出所有的把字句：
      ```
      你_Nh 要_D 把_P 重心_Na 置於_VC 家人_Na 身_Na 上_Ncd ，_COMMACATEGORY
      而_Cbb 不_D 是_SHI 把_P 重心_Na 放_VC 在_P 工作_VA 。_PERIODCATEGORY
      整_Neqa 天_Nf 把_P 心思_Na 放_VC 在_P 工作_Na 卻_D 不管_Cbb 家人_Na 實在_D 很_Dfa 糟_VH
      應該_D 多_D 把_P 時間_Na 花_VC 在_P 有_V_2 意義_Na 的_DE 事情_Na 上_Ng
      ```
    - 比較精準的方式是使用[漢唐與琼玉介紹的方式](https://docs.google.com/presentation/d/1c_xfgZI5YUCJSanj7l_E9O_0MYGOlZD1vqFSuv6Rp0I)，以比較複雜的資料結構去表徵語料(建立微語料庫)，再透過程式實作簡單的語料查詢功能
