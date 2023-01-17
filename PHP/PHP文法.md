## phpの基本文法
~~~php
<?php
// 文字表示
echo('test');
echo('<br>');

// 変数宣言(動的型付け)
// 先頭は英文字か_
$test_1 = 123;
$test_2 = 456;
$test_3 = $test_1 . $test_2;

// 定数宣言
const TEST = 'test';

// 型確認
var_dump($test_3);

//　配列宣言
$array_1 = [1, 2, 3];
$array_2 = [[4, 5, 6], [7, 8, 9]];

// 配列の要素確認
echo('<pre>');
var_dump($array_1);
echo('</pre>');

echo($array_2[0][1])

// 連想配列宣言
$array_members = [
    'name' => '本田', 
    'height' => 170, 
    'hobby' => 'サッカー'
    ];

echo($array_members['hobby']);

$array_member2 = [
    '本田' => [
        'height' => 170,
        'hobby' => 'サッカー'
    ],
    '香川' => [
        'height' => 165,
        'hobby' => 'サッカー'
    ]
];

echo($array_member2['香川']['hobby']);

// if文
// === 型も同じ
if ()
{

} 
else if ()
{

} 
else
{

}

// 三項演算子
$number = 1;
$answer = $number === 1 ? '正解' : '不正解';

// foreach文
// valueのみ表示
foreach ($array_members as $array_member)
{
    echo $array_member;
}

// keyとvalueを表示
foreach ($array_members as $key => $value)
{
    echo $key . 'は' . $value . 'です';
}

// for文
for ($i = 0; $i < 10; $i++)
{
    echo $i;
}

// while文
$j = 0;
while ($j < 5>)
{
    echo $j;
    $j++;
}

// switch文
// switch文では==判定される
$data = 0;
switch ($data)
{
    case $data === 0:
        echo '0です';
        break;
    case 1:
        echo '1です';
        break;
    default:
        echo 'エラー';
}

// 関数宣言
function add($num1, $num2)
{
    $num3 = $num1 + $num2;
    return $num3;
}

echo add(10, 20);

// 文字列長さ取得
$text = '123';
echo strlen($text);

// マルチバイト（英数字以外）
$text2 = 'アイウエオ';
echo mb_strlen($text2);

// 文字列の置換
$text3 = '文字列の置換';
echo str_replace('置換', 'ちかん', $text3);

// 指定文字列で分割
$text4 = '指定文字列で，分割します';
var_dump(explode('，', $text4));

// 正規表現
$text5 = '特定の文字列が含まれているか確認する';
// 含まれていれば1が返ってくる
echo preg_match('/文字列/', $text5);

// 指定文字列から文字列を取得する
echo substr('12345', 2);
echo mb_substr('アイウエオ', 3);

// 配列に要素を追加する
array_push($array_1, 3, 4);

// ファイルの読み込み
require 'ファイルパス';

// 絶対パス表示
echo __DIR__;
echo __FILE__;

?>
~~~