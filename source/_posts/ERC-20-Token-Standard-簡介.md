---
title: ERC-20 Token Standard 簡介
date: 2020-05-11 09:33:25
tags: 
- ERC-20
- ERC-721
- Solidity
---

## ERC-20 與 ERC-721 比較

![](https://i.imgur.com/yJRa1ri.png)

簡單來說，ERC20是「每個代幣都一樣」；而ERC721則是「每個代幣都有其獨特性」

## Interface
```Solidity
contract ERC20Interface {
    function totalSupply() public constant returns (uint);
    function balanceOf(address tokenOwner) public constant returns (uint balance);
    function allowance(address tokenOwner, address spender) public constant returns (uint remaining);
    function transfer(address to, uint tokens) public returns (bool success);
    function approve(address spender, uint tokens) public returns (bool success);
    function transferFrom(address from, address to, uint tokens) public returns (bool success);

    event Transfer(address indexed from, address indexed to, uint tokens);
    event Approval(address indexed tokenOwner, address indexed spender, uint tokens);
}
```

總共有6個function以及2個event。其中constant的function是唯讀的，所以不會花費Gas。
Event只用於記錄，可以視為一般系統上的log功能。

```
string public constant name = "Token Name";
string public constant symbol = "SYM";
uint8 public constant decimals = 18; // 18 is the most common number of decimal places
```

另外還有三個需要設定的參數：name、symbol、decimals。name是Token的名字；symbol是Token的代稱（簡稱）；decimals是Token小數最多可以到幾位數，正常為18，也就是和Ether一樣。

## Function 說明

1. totalSupply()，Token的發行總量。
2. balanceOf(address)，傳入地址的錢包的Token數量。
3. allowance(address A, address B)，A批准給B的Token量。
4. transfer(address A, uint num)，將數量為num的Token轉移給A。
5. approve(address A, uint num)，批准數量為num的Token轉移給A，需注意的是，這個function只是單純做「批准」這個動作，而沒有進行轉移。若需要轉移則要再呼叫transferFrom。
6. transferFrom(address, address, uint)，將數量為num的Token由A轉移給B。


## 注意事項

Solidity版本 >= 0.4.17


## Ref.

- [ERC20, ERC721比較](https://medium.com/7sevencoin/erc20%E5%92%8Cerc721%E4%B8%8D%E4%B8%80%E6%A8%A3%E5%9C%A8%E5%93%AA%E8%A3%A1-2e550bb0bea3)
- [ERC-20標準doc](https://eips.ethereum.org/EIPS/eip-20)
