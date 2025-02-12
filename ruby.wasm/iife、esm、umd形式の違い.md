# IIFE形式(Immediately Invoked Function Expression)
即時実行関数式でスクリプトが読み込まれた時点でその場で即座に実行される。

ruby.wasm ではブラウザからシンプルに Ruby スクリプトを呼びたいときに使う。

```html
<html>
  <script src="https://cdn.jsdelivr.net/npm/@ruby/3.4-wasm-wasi@2.7.1/dist/browser.script.iife.js"></script>
  <script type="text/ruby">
    require "js"

    puts RUBY_VERSION # (Printed to the Web browser console)
    JS.global[:document].write "Hello, world!"
  </script>
</html>
```

# ESM形式(ECMAScript Modules)
ES Modules はモダンなブラウザや Node.js で利用される標準のモジュール形式。

ruby.wasm ではモジュール形式の JavaScript から Ruby VM を制御したいときに使う。

```html
<html>
  <script type="module">
    import { DefaultRubyVM } from "https://cdn.jsdelivr.net/npm/@ruby/wasm-wasi@2.7.1/dist/browser/+esm";
    const response = await fetch("https://cdn.jsdelivr.net/npm/@ruby/3.4-wasm-wasi@2.7.1/dist/ruby+stdlib.wasm");
    const module = await WebAssembly.compileStreaming(response);
    const { vm } = await DefaultRubyVM(module);

    vm.eval(`
      require "js"
      JS.global[:document].write "Hello, world!"
    `);
  </script>
</html>
```

# UMD形式(Universal Module Definition)
レガシー環境との互換性を重視した形式。

ruby.wasm ではレガシーな JavaScript から Ruby VM を制御したいときに使う。

```html
<html>
  <script src="https://cdn.jsdelivr.net/npm/@ruby/wasm-wasi@2.7.1/dist/browser.umd.js"></script>
  <script>
    const main = async () => {
      const { DefaultRubyVM } = window["ruby-wasm-wasi"];
      const response = await fetch("https://cdn.jsdelivr.net/npm/@ruby/3.4-wasm-wasi@2.7.1/dist/ruby+stdlib.wasm");
      const module = await WebAssembly.compileStreaming(response);
      const { vm } = await DefaultRubyVM(module);

      vm.eval(`
        require "js"
        JS.global[:document].write "Hello, world!"
      `);
    }
    main()
  </script>
</html>
```

https://github.com/ruby/ruby.wasm/blob/main/docs/cheat_sheet.md