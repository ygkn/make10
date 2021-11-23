# make10
make10 パズルを解くプログラム
> make10 (テンパズル) は，4桁の数字を1桁の数字4つとみなし，これに四則演算を用いて10を作る遊び

## 方針
1. 場合の数を全て列挙して逆ポーランド記法(RPN)で表現する

   - n 桁の中から2つ選び，n-1 桁の数に減らす
   - これを n=1 になるまで繰り返す
```
["1", "2", "3", "4"]
↓
["1 2 +", "3", "4"]
↓
["1 2 + 3 +", "4"]
↓
["1 2 + 3 + 4 +"]
```

2. RPN 式を計算して 10 になる RPN 式のみ保持する
3. RPN を中置記法に変換する

### 場合の数
入力が 4 桁の場合は `(4C2 * 6 ) * (3C2 * 6 ) * (2C2 * 6) = 3888`，
一般解では ![\prod_{k=2}^{n}(_k C _2 \times 6)](images/math-1.svg)
となるが，重複を除去するとこれより小さい値になる．

## 入出力
| 入力                    | 出力                                          |
| ----------------------- | --------------------------------------------- |
| `["1","3","4","7"]`     | `["((3-1)*7)-4","((7-4)*3)+1","1-((4-7)*3)"]` |
| `["1","1","9","9"]`     | `["((1/9)+1)*9"]`                             |
| `["2","5"]`             | `["2*5"]`                                     |
| `["1","2","4"]`         | `["(1+4)*2"]`                                 |
| `["5","9","9","9","9"]` | `["((9/9)+(9/9))*5"]`                         |


## 実行
```sh
git clone <this repo>
cd <this repo>
yarn install
ts-node src/example.ts
```
