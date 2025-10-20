---
sort: 1
---
# ルートモデルバインディング

前回の[モデル、コントローラ](../shop_item_index/README.md)の章では、サンプルとして、`items`テーブルからすべての商品情報を取得し、一覧を表示しました。
今回は、ある特定の商品情報を取得して表示する方法を学びます。

Laravelの中でもやり方は色々ありますが、今回は**ルートモデルバインディング**を使って、商品番号に対応する商品情報を取得します。

## ルーティングの修正

今回のサンプル用のルーティングを`routes/web.php`に追加しますが、今までとは少し異なる書き方があります。

```php
use Illuminate\Support\Facades\Route;
use App\Http\Controllers\ItemController;

// 途中省略


Route::get('item', [ItemController::class, 'index'])->name('item.index');
// --- 以下を追加 ---  
Route::get('item/show/{item}', [ItemController::class, 'show'])->name('item.show');
```

**【解説】**

`Route::get('item/show/{item}', [ItemController::class, 'show'])->name('item.show');`: <br>
`item/show/{item}`は、商品詳細画面に遷移するためのURLです。
URLの末尾に`/{item}`が付いているのは、商品番号を指定するためです。

PHPでいうところの、GETリクエスト時のクエリパラメータに相当します。
`{item}`は、商品番号を表しています。

ここで大事なのではなぜ商品番号を指定したいのに、`{item}`という名前なのかです。
これは、**ルートモデルバインディングを使うためのルール**です。
ルートモデルバインディングを使う場合、ルーティングの定義とコントローラのメソッドの引数名が一致している必要があります。
詳細はコントローラの修正で説明します。

`[ItemController::class, 'show']`は、`ItemController`クラスの`show`メソッドを呼び出すことを意味します。
