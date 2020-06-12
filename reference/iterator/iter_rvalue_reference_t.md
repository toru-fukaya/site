# iter_rvalue_reference_t
* iterator[meta header]
* std[meta namespace]
* type-alias[meta id-type]
* cpp20[meta cpp]

```cpp
namespace std {
  template<dereferenceable I>
    requires requires(I& i) {
      { ranges::iter_move(i) } -> can-reference;
    }
  using iter_rvalue_reference_t = decltype(ranges::iter_move(declval<I&>()));
}
```
* dereferenceable[link /reference/iterator/exposition_only.md]
* can-reference[link /reference/iterator/exposition_only.md.nolink]
* iter_move[link /reference/iterator/iter_move.md.nolink]
* declval[link /reference/utility/declval.md]

## 概要

任意のイテレータ型`I`から、そのイテレータの要素への右辺値参照型を取得する。

## 例
```cpp example
#include <iostream>
#include <iterator>
#include <vector>

int main() {
  using vec_iterator = std::vector<int>::iterator;
  using pointer = double*;

  static_assert(std::same_as<std::iter_rvalue_reference_t<vec_iterator>, int&&>);
  static_assert(std::same_as<std::iter_rvalue_reference_t<pointer>     , double&&>);
}
```
* std::iter_rvalue_reference_t[color ff0000]

### 出力
```
```

## バージョン
### 言語
- C++20

### 処理系
- [Clang](/implementation.md#clang): ??
- [GCC](/implementation.md#gcc): 10.1
- [Visual C++](/implementation.md#visual_cpp): 2019 Update 6

## 関連項目

- [`iterator_traits`](iterator_traits.md)

## 参照

- [P0896R4 The One Ranges Proposal (was Merging the Ranges TS)](http://www.open-std.org/jtc1/sc22/wg21/docs/papers/2018/p0896r4.pdf)