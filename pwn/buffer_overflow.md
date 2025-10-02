# Buffer overflow
バッファサイズ超過によるリターンアドレスの上書き

- canary
- ASLR
- NX bit </br>
などの防御機構がある。

```C
void vuln() {
    char buf[64];
    gets(buf); // ここで入力サイズを制限していないのが原因
}
```
## よくある組合せ
- gdbでスタック構造を確認
- pattern_create.rbでオフセット特定
- pwntoolsでROPチェーン構築
