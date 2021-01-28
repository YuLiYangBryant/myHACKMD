# PHPMyAdmin相關bug處理

1. Notice in ./libraries/DisplayResults.php#xxxx
 Trying to access array offset on value of type bool
 
 You can edit the file /usr/share/phpmyadmin/libraries/DisplayResults.php
in the specific line #XXXX Search

把 `col_visib[$j] 後面加上 ?? false`
像這樣-> `col_visib[$j] ?? false`
## 

2. ErrorException : implode(): Passing glue string after array is deprecated. Swap the parameters

錯誤發生在/usr/share/phpmyadmin/js/get_image.js.php #72
找到相關的implode()函式
原本寫法：`<?php echo implode($keys, ",\n        ") , "\n"; ?>`
將implode內的兩個變數交換
後來寫法：`<?php echo implode(",\n        ", $keys) , "\n"; ?>`
## 

3. Warning in ./libraries/plugin_interface.lib.php#551
 count(): Parameter must be an array or an object that implements Countable
 
 原本寫法：`if ($options != null && count($options) > 0) {`
 後來寫法：`if ($options != null && count((array)$options) > 0) {`
 加上一個(array)

## 

4. Warning in ./libraries/sql.lib.php#613
 count(): Parameter must be an array or an object that implements Countable
 
原本：`(count($analyzed_sql_results[‘select_expr’] == 1)`
改成：`((count($analyzed_sql_results[‘select_expr’]) == 1)`


##  
尚未設定 phpMyAdmin 設定儲存空間，部份延伸功能將無法使用。 了解原因。
或者前往任一個資料庫的 '操作' 頁籤設定。

1. 上mariadb 新增資料庫 phpmyadmin
2. 匯入 phpMyAdmin/sql/create_tables.sql 便會自動建立一個 phpmyadmin 資料庫,裡面有這些資料表, 再來新增一個能夠存取此資料庫的帳號
3. 新增phpmyadmin為帳戶，許可權設置為GRANT SELECT, INSERT, DELETE, UPDATE