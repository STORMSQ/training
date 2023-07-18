# 練習1 Javascript基本語法

```javascript
function myfunction(){
    var num = 10 //定義一個數字
    var studentName = '張三' //定義一個學生名稱
    
    Logger.log(num)
    Logger.log(studentName) //分別打印出結果
    
    //試著調用其他函數
    var resultName = numberAddTen(num) //把num這個變量當參數傳進去
    var resultStudentName =changeStudentNamePrefix(studentName) //把studentName當參數傳進去
    
    Logger.log(resultName)
    Logger.log(resultStudentName)
}

/**
 *  數字增加10的方法
 */
function numberAddTen(number){
    return number+10
}

/**
 *  學生名稱添加%前綴的方法
 */
function changeStudentNamePrefix(student_name)
{
    return '%'+student_name
}
```



# 練習2 操作App Script專案 



1. 創建一個空白試算表

2. 在試算表中填入資料

   | 學號       | 姓名 |
   | ---------- | ---- |
   | A123456789 | 張三 |
   | A123456785 | 李四 |
   | A123456856 | 王五 |
   | A225314582 | 孫六 |
   | A125478961 | 錢七 |

   

3. 重新命名工作表為student

4. 擴充功能 > App Script

5. 開始編寫程式



## 初始化

```javascript
function test1() {
  let id ='1zUyFT_UUOnDNGDVtnnQtoxGod5ouIz58YHmd6crFkzc' //試算表ID
  let sheet = SpreadsheetApp.openById(id).getSheetByName('student'); //獲取該試算表下名為student的工作表

}
```



## 取值

```javascript
function test2() {
  let id ='1zUyFT_UUOnDNGDVtnnQtoxGod5ouIz58YHmd6crFkzc' //試算表ID
  let sheet = SpreadsheetApp.openById(id).getSheetByName('student'); //獲取該試算表下名為student的工作表

  let last = sheet.getLastRow()

  let result = sheet.getRange("a2:b5").getValues()

  Logger.log(result) //我們用logger獲取資料

}

```

## 使用

```javascript
function test3() {
  let id ='1zUyFT_UUOnDNGDVtnnQtoxGod5ouIz58YHmd6crFkzc' //試算表ID
  let sheet = SpreadsheetApp.openById(id).getSheetByName('student'); //獲取該試算表下名為student的工作表

  let last = sheet.getLastRow()

  let result = sheet.getRange("a2:b5").getValues()

  /**
   * 
   * 多維陣列如何取裡面的東西呢，我們先把剛剛打印出來的結果上點給人看的標籤
   * [
   *    0=>[0=>A123456789, 1=>張三],
   *    1=>[0=>A123456785, 1=>李四],
   *    2=>[0=>A123456856, 1=>王五],
   *    3=>[0=>A225314582, 1=>孫六]
   * ]
   * 緊接著取陣列資料可以使用 變量+[](可多個方括號) 來取
   * 
   * 
   * 假設我們要取 王五 這筆資料，則使用 result[2][1]
   * 先看看result[2] 代表取到 整個資料中的位置為 2 筆的資料，即 [0=>A123456856, 1=>王五] 這筆， 然後後面的[1]，則表示 在這個結果之下，再取位置為1的這筆資料
   * 
   * 
   *  試著取看看其他筆資料吧
   * */

  Logger.log(result[0][1])

}

```

## 寫值

```javascript
function test4() {
  let id ='1zUyFT_UUOnDNGDVtnnQtoxGod5ouIz58YHmd6crFkzc' //試算表ID
  let sheet = SpreadsheetApp.openById(id).getSheetByName('student'); //獲取該試算表下名為student的工作表

  let last = sheet.getLastRow() //一樣需要獲取最後一欄是哪一欄

/**
 * 多行寫入需要自己造 陣列
 * 回顧剛剛解釋的陣列範例，其中一行長這樣，現在我們現在需要自己製造一個陣列 傳遞給寫入函數
 * 
 *  3=>[0=>A225314582, 1=>孫六]
 * 
 *  宣告一個陣列
 *  let data = []
 *  填入資料 ['1','2','3','4','張三','李四']
 *  注意：陣列的正確寫法是 文字部分需要加入"" or ''
 *  純數字可以不用加雙引號或單引號
 *  值和值之間使用 逗號 分隔
 * 
 * 
 */
  sheet.appendRow([
    'A125478961',
    '錢七'
  ])
```

## 修改資料

```javascript
function test5() {
  let id ='1zUyFT_UUOnDNGDVtnnQtoxGod5ouIz58YHmd6crFkzc' //試算表ID
  let sheet = SpreadsheetApp.openById(id).getSheetByName('student'); //獲取該試算表下名為student的工作表
 

  /**
   *  修改資料是 找資料 和 寫資料的綜合練習
   * 
   *   先找範圍 然後使用 setValue
   *  
   *  小提示：getRange() 除了可以使用確切的儲存格編號，也可使用行列表示確切儲存格
   *  sheet.getRange(4,2) 第四行第二列
   */


   let change = '孫大千'
   sheet.getRange("b5").setValue(change)
    

  
}
```

