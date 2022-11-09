## LINQとは
コレクション（配列、List、Dictionaryなど）の要素を処理するメソッドを集めたライブラリ

## Selectメソッド
コレクションの要素全てに対して、引数でラムダ式で指定した関数の処理を行える関数

~~~csharp
using System;
using System.Linq;

class Sample
{
    static void Main()
    {
        int[] src = {1, 2, 3, 4, 5, 6};

        var query = src.Select(x => x % 3);
        Console.WriteLine("[{0}]", string.Join(" ", query));

        Console.ReadKey();
    }
}
~~~

~~~csharp
[0, 1, 2, 0, 1, 2]
~~~

## Whereオペレータ
Whereオペレータを使うことで、条件を満たす要素のみSelectメソッドで処理することができる

~~~csharp
using System;
using System.Linq;

class Sample
{
    static void Main()
    {
        int[] src = {1, 2, 3, 4, 5, 6};

        var query = src
        .Where(x => x > 1 && x < 5)
        .Select(x => x % 3);
        Console.WriteLine("[{0}]", string.Join(" ", query));

        Console.ReadKey();
    }
}
~~~

~~~csharp
[2, 0, 1]
~~~
