# controljs
一个简单的流程控制库  

> 当商品的优惠政策需求频繁变动时，可以把每个优惠政策写成一个算法类，该算法类有 order属性（排序），enable属性（是否启用），install方法（执行方法），然后把算法类推入列队里，最后由执行类（controljs）执行。
> 执行过程会把算法类先按order值排序，然后每执行一个算法类就把上一个执行结果返回给下一个算法类，最后输出最终值

```javascript 

import Control from './controljs'

let t1 = {
  order: 100,
  enable: true,
  install(newV) {
    console.log('减100')
    return newV - 100;
  }
}

let t2 = {
  order: 200,
  enable: false,
  install(newV) {
    console.log('打7折')
    return newV * 0.7;
  }
}
const test1 = new Control(5625, [t1, t2]);
test1.run().then(res => {
  console.log('最终价格', res);
})

```