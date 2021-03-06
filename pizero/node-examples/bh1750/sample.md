# BH1750 光センサー

## 配線図

![配線図](./schematic.png "schematic")

# ドライバのインストール

```
npm i @chirimen/bh1750
```

# サンプルコード

```javascript
const { requestI2CAccess } = require("node-web-i2c");
const BH1750 = require("@chirimen/bh1750");
const { promisify } = require("util");
const sleep = promisify(setTimeout);

main();

async function main() {
  const i2cAccess = await requestI2CAccess();
  const port = i2cAccess.ports.get(1);
  const bh1750 = new BH1750(port, 0x23);
  await bh1750.init();

  while (true) {
    const lux = await bh1750.measure_high_res();
    console.log(lux.toFixed(3) + "lx");

    await sleep(500);
  }
}
```

