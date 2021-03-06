# 発展的な知識（教科書20章）

- ＜目次＞
  - <a href="#20.1">クラスメンバについて理解する（20.1節）</a>
  - <a href="#20.2">フィールドの隠蔽（20.2節）</a>　＊省略
  - <a href="#20.3">インタフェースの文法（20.3節）</a>　＊省略
  - <a href="#20.1">配列の配列（20.4節）</a>　＊省略
  - <a href="#20.5">ファイルとプログラムの実行（20.5節）</a>

<hr>

## <a name="20.1">クラスメンバについて理解する（20.1節）</a>
- インスタンスメンバとstaticメンバ
  - 詳細解説: 教科書 pp.484-
    - 要点
      - フィールド変数とメソッドには「staticが付いてるか否か」で、JVMによる実体化方法が異なる。
        - staticメンバ（変数もメソッドも）は、クラスが初めて使用される時に実行直前に実体化される。new演算子でインスタンス生成せずとも利用できる。言い換えると **「初めてクラスを利用する際にのみ実体化される」ことに注意。インスタンスを生成しても、staticメンバは最初に実体化したものが再利用され続ける**。staticメンバは常に同じ実体が参照される。(one for each class)
          - staticメソッドはインスタンスメンバにアクセスできない
          - staticメソッドはthisを使えない
        - インスタンスメンバ（static付いていない変数とメソッド）は、new演算子でインスタンス生成されるまでは実体化されない。インスタンス生成する度に実体を作成していしているため、インスタンスごとに参照される実体が異なる。(many for each class)
- staticメンバの例: [java.lang.Math](http://docs.oracle.com/javase/9/docs/api/java/lang/Math.html)
  - Math.E や Math.PI といったstaticなフィールド変数は、Mathクラスのオブジェクトを生成しなくても利用できる。
    - 初めてMathクラス利用する際に、自動で実体化してくれる。
  - 同様に、Math.abs() といったstaticなメソッドも、Mathクラスのオブジェクトを生成しなくても利用できる。
- 疑問点「全てstaticメンバにしてしまえば良いのでは？」
  - staticメンバの主な利点
    - インスタンスを用意せずとも利用できる。（インスタンスから独立した機能を提供できる）
    - 1つのオブジェクトしか用意させたくない時に、それを強制できる。
  - staticメンバの主な欠点
    - 1つしか実体化できない。（そのためのもの）
      - 一度実体化されると「いついかなる時でも1つしか実体がない」ため、そのことを踏まえた実装にしないとトラブルの種になることがある。
    - 「staticメンバ（変数もメソッドも）は、クラスが初めて使用される時に実行直前に実体化される」ので、不必要にメモリを消費してしまう。
      - そのため、利用率が高く、メモリ消費も小さいメンバを選別して static にすることが多い。
- どういうときに static を使うべきか？
  - staticを使うのは、「staticじゃないと実現困難な場合」に限定したほうが良い。

<hr>

## <a name="20.2">フィールドの隠蔽（20.2節）</a>
- 省略（興味がある人は読んでみよう）
  - メソッドには @Override がある。変数はどうだろう？という話。

<hr>

## <a name="20.3">インタフェースの文法（20.3節）</a>
- 省略（興味がある人は読んでみよう）
  - Java8からは、インタフェースに限定的に実装も含めることができるという話。

<hr>

## <a name="20.1">配列の配列（20.4節）</a>
- 教科書 pp.501-

```
/* ただの配列 */
int[] a = {1, 2};
int[] b = {3, 4, 5, 6};
int[] c = {7, 8, 9};

/* 上記のような「配列」を要素として持つ配列 */
//case1:
//初期化リストで作成する例
int[][] numbers = { {1,2},{3,4,5,6},{7,8,9}};
//最初の[]が、numbersから見た要素のインデックス。
//2番目の[]は、各要素内のインデックス。
//例えば numbers[0][1] は、「numbers[0]の1番目の要素」を参照することになる。

//case2:
//最初に全体を保管する配列だけ先に用意し、後で個別にnewする例
int[][] numbers = new int[3][];
numbers[0] = new int[]{1,2};
numbers[1] = new int[]{3,4,5,6};
numbers[2] = new int[]{7,8,9};

//case3:
//個々の配列要素数が決まってるなら、先に要素数を指定して初期化できる。
int[][] numbers = new int[3][4];
//初期化した後は numbers[0][1] = 1; のように更新可能。
```

<hr>

## <a name="20.5">ファイルとプログラムの実行（20.5節）</a>
- Javaファイルと実行に関する規則, p.507
  - 省略。ファイル名/classファイル/packageについて整理されてます。
- コマンドライン引数, p.508
```
public class Exec {
    public static void main(String[] args){
        System.out.println("args[0] = " + args[0]);
        int val = Integer.parseInt(args[1]);
        System.out.println("args[1] = " + args[1]);
    }
}
```
