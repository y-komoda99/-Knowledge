# Zenject
1. [Zenjectとは](#zenjectとは)
2. [Zenjectの使い方](#zenjectの使い方)
    1. [Zenjectのインストール](#zenjectのインストール)
    2. [クラス作成](#クラス作成)
    3. [Installer作成](#installer作成)
    4. [Context作成](#context作成)

## Zenjectとは
依存性注入（DI）のためのライブラリ
~~~csharp
public interface IExample {}

public class Example : IExample {}
~~~
~~~csharp
public class Injected : MonoBehaviour
{
    private IExample _Example;
}
~~~
`Injected`と`Example`を疎結合にする（`Injected`の中で、`_Example = new Example()`とインスタンスを生成し、参照を持ちたくない）時に、Zenjectを使うと、`Injected`に`Example`のインスタンスが注入され、`Injected`は`IExample`しか知らなくて良いという風に疎結合が保たれる。

## Zenjectの使い方
### Zenjectのインストール
`Unity`の`Asset Store`からZenjectを検索し、インストールする。
`Assets > Plugins > Zenject`というフォルダが作成される。

### クラス作成
~~~csharp
using UnityEngine;
using Zenject;

// Injectedが知ることのできるインターフェース（必須ではない）
public interface IExample {}

// Injectedに注入されるクラス
public class Example : IExample {}

// Exampleを注入するクラス
public class Injected : MonoBehaviour
{
    // [Inject]アトリビュートをつける
    [Inject]
    private IExample _Example;
}
~~~

### Installer作成
~~~csharp
using UnityEngine;
using Zenject;

public class ExampleInstaller : MonoInstaller
{
    public override void InstallBindings()
    {
        Container
        .Bind<IExample>() //　この型で定義されたフィールドに
        .To<Example>() // この型のインスタンスを注入する
        .AsSingle(); // インスタンスを再利用するかの設定
    }
}
~~~
`Bind<T>()`は依存性を注入する対象の型を指定するためのメソッドで、このクラスまたはインターフェースガ定義され、`[Inject]`アトリビュートがついているフィールドに注入される。

`To<T>()`は実際に注入する方を指定するメソッドで、`Bind<T>()`の指定した型と同じならば省略可能。

|メソッド名|説明|
|---|:---|
|AsTranslent()|インスタンスを再利用しない|
|AsCached()|インスタンスを再利用する|
|AsSingle()|インスタンスを再利用する<br>2回以上`Bind<T>()`されると例外発生するため、シングルトンにしたいオブジェクトに定義する|

### Context作成
Unity上で、`Hierarchyを右クリック > Zenject > SceneContext`を選択する。<br>生成されたGameObjectに`ExampleInstaller`をアタッチし、`SceneContext`の`MonoInstallers`に代入する。

`Context`は`Installer`が影響する範囲を指定するためのものである。