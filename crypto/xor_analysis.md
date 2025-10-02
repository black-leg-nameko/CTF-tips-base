# XOR解析
XORは暗号分野で頻出する演算。暗号文が同じ鍵でXORされた場合、平文同士のXORによる平文推測が可能。

## 例
C1 = P1 ~ K </br>
C2 = P2 ~ K </br>
(暗号鍵Kが共通している) </br>
このとき </br>
C1 ~ C2 = (P1 ~ K) ~ (P2 ~ K) = P1 ~ P2 </br>
(同じ引数でXORを二回適用すると元に戻るため) </br>
つまり、P1かP2のどちらかがわかればもう片方のひらぶんが推測できる. </br>

応用先としてWPA2のKRACK攻撃, Known Plaintext Attack, Reused Key Attack, One-Time Padの誤用検出がある。</br>



## PythonでのXOR解析script
```python
def xor_bytes(b1, b2):
    return bytes([x ^ y for x, y in zip(b1, b2)])

c1 = bytes.fromhex("1a2b3c4d")
c2 = bytes.fromhex("0f1e2d3c")
print(xor_bytes(c1, c2).hex())
```
