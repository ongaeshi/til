vm.eval 中に Rubyの例外が発生すると [RbError](https://github.com/ruby/ruby.wasm/blob/da8e6038cbabacec46814ab990dfa436db141c13/packages/npm-packages/ruby-wasm-wasi/src/vm.ts#L1015)が throw されるので catch して DOM に出力する。

```html
<html>
  <script type="module">
    import { DefaultRubyVM } from "https://cdn.jsdelivr.net/npm/@ruby/wasm-wasi@2.7.1/dist/browser/+esm";
    const response = await fetch("https://cdn.jsdelivr.net/npm/@ruby/3.4-wasm-wasi@2.7.1/dist/ruby+stdlib.wasm");
    const module = await WebAssembly.compileStreaming(response);
    const { vm } = await DefaultRubyVM(module);

    try {
      vm.eval("doSomeMethod()");
    } catch (e) {
      document.getElementById("error-console").value += e.message + "\n";
    }
  </script>
  <textarea id="error-console" readonly></textarea>
</html>
```

https://github.com/ruby/ruby.wasm/blob/main/docs/cheat_sheet.md#browser

