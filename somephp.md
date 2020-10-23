# PHP
# 分頁
## 同步換頁
七個步驟w：
1. 連上資料庫　　　(books)
2. 資料筆數　　　　(7本)
3. 一頁要幾筆資料　(2筆)
4. 共有幾頁　　　　(7本÷2筆=要4頁)
5. 顯示頁面　　　　(定義變數(我在第幾頁))
6. 取得當前頁面資料(FETCH資料)
7. 在頁面上呈現資料(<?=$ooxx["bookname"]?>)

以書籍電商為範例：
1. 連上資料庫
    ```php
    $dsn      = "mysql:host=localhost;port=3306;dbname=資料庫名稱;charset=utf8";
	$user     = "使用者名稱";
	$password = "使用者密碼";
	$options  = array(PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION);
	$pdo      = new PDO($dsn, $user, $password, $options);
    ```
2. 取得資料筆數
    ```php
    $sql = "select count(*) totalCount from products";
	$stmt = $pdo->query($sql);
	$row = $stmt->fetch(PDO::FETCH_ASSOC);
	$totalRecords = $row["totalCount"];//這是別名(可以用)
    ```
3. 定義一頁要幾筆資料
    ```php
    $recPerPage = 2;
    ```
4. 計算共有幾頁
    ```php
    $totalPages = ceil($totalRecords / $recPerPage);
    ```
5. 定義顯示頁面
    ```php
    $pageNo = isset($_GET["pageNo"]) ? $_GET["pageNo"] : 1;
    ```
6. 取得當前頁面資料
    ```php
    $start = ($pageNo-1) * $recPerPage;	
	$sql = "select * from products limit $start, $recPerPage";
	$products = $pdo->query($sql);
	$prodRows = $products->fetchAll(PDO::FETCH_ASSOC);
    ```
7. 在頁面上呈現資料
    ```php
    <table align='center' width="800">
	<tr bgcolor="#bfbfef"><th>書號</th><th>書名</th><th>價格</th><th>作者</th></tr>
	<?php
	foreach($prodRows as $i=>$prodRow){//當抓得到一筆資料
	?>
		<tr>
		<td><?=$prodRow["psn"]?></td>
		<td><?=$prodRow["pname"]?></td>
		<td><?=$prodRow["price"]?></td>
		<td><?=$prodRow["author"]?></td>
		</tr>
	<?php
	}
	?>
	</table> 
    <center>
    <?php 
    //顯示可以瀏覽其它頁的連結

    for($i=1; $i<=$totalPages; $i++){
        echo "<a href='paging.php?pageNo=$i'>$i</a>&nbsp;&nbsp;"; 

    }
    ?>
    </center>
    ```