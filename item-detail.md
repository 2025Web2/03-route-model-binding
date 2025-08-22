# 商品一覧画面の修正

次に、前回の[モデル、コントローラ](https://2025web2.github.io/02-model-controller/)の章で作成した商品の一覧画面に詳細のリンクを追加し、一覧から詳細データが見えるようにしましょう。

`resources/views/item/index.blade.php`を以下のように修正してください。

{% raw %}
```php
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>サンプル</title>
</head>
<body>
<h3>商品一覧</h3>
    <table>
        <tr>
            <th>商品名</th>
            <th>価格</th>
        </tr>
    @foreach( $items  as  $item )
        <tr>
            <td class="td_item_name"> {{  $item->name }} </td>
            <td class="td_right">&yen; {{  number_format( $item->price) }} </td>
            <!-- 以下を追加 -->
            <td><a href="{{ route('item.show',  ['item' => $item->ident]) }}">詳細</a></td>
            <!-- ここまで -->
        </tr>
    @endforeach
    </table>
</body>
</html>
```


**【解説】**

`<a href="{{ route('item.show',  ['item' => $item->ident]) }}">詳細</a>`: <br>
商品詳細画面に遷移するためのリンクです。
`route('item.show',  ['item' => $item->ident])`は、商品詳細画面に遷移するためのURLを生成しています。
`['item' => $item->ident]`は、itemという名前で指定した商品番号が、ルーティングで設定された`Route::get('item/show/{item}', [ItemController::class, 'show']);`の`{item}`に渡されます。