# -questions：（来源：https://github.com/yygmind/blog/issues/43）
1.（滴滴、饿了么）写 React / Vue 项目时为什么要在列表组件中写 key，其作用是什么？

  我答：key可以用来唯一标识列表中的节点。当更新时，react会先生成虚拟dom，然后比较之前的dom，比较时是利用key值来确定比较的对象，从而只更新更改过的部分。

  标答：vue和react都是采用diff算法来对比新旧虚拟节点，从而更新节点。在vue的diff函数中（建议先了解一下diff算法过程）。
      在交叉对比中，当新节点跟旧节点头尾交叉对比没有结果时，会根据新节点的key去对比旧节点数组中的key，从而找到相应旧节点（这里对应的是一个key => index 的map映射）。如果没找到就认为是一个新增节点。而如果没有key，那么就会采用遍历查找的方式去找到对应的旧节点。一种一个map映射，另一种是遍历查找。相比而言。map映射的速度更快。
  
      key是给每一个vnode的唯一id,可以依靠key,更准确, 更快的拿到oldVnode中对应的vnode节点。
      1. 更准确
      因为带key就不是就地复用了，在sameNode函数 a.key === b.key对比中可以避免就地复用的情况。所以会更加准确。
      2. 更快
      利用key的唯一性生成map对象来获取对应节点，比遍历方式更快。(这个观点，就是我最初的那个观点。从这个角度看，map会比遍历更快。)

  记忆：diff算法对比新旧虚拟节点来更新节点、根据新节点key找旧节点；无key则是遍历算法
  
  延伸知识：diff算法


2.['1', '2', '3'].map(parseInt) what & why ?
  
  我答：答不出来
  标答：首先让我们回顾一下，map函数的第一个参数callback：
      var new_array = arr.map(function callback(currentValue[, index[, array]]) { // Return element for new_array }[, thisArg])
      这个callback一共可以接收三个参数，其中第一个参数代表当前被处理的元素，而第二个参数代表该元素的索引。
      而parseInt则是用来解析字符串的，使字符串成为指定基数的整数。
      parseInt(string, radix)
      接收两个参数，第一个表示被处理的值（字符串），第二个表示为解析时的基数。

      parseInt('1', 0) //radix为0时，且string参数不以“0x”和“0”开头时，按照10为基数处理。这个时候返回1
      parseInt('2', 1) //基数为1（1进制）表示的数中，最大值小于2，所以无法解析，返回NaN
      parseInt('3', 2) //基数为2（2进制）表示的数中，最大值小于3，所以无法解析，返回NaN


3.什么是防抖和节流？有什么区别？如何实现？
  
  我答：不知

  标答：1.防抖
       触发高频事件后n秒内函数只会执行一次，如果n秒内高频事件再次被触发，则重新计算时间
       2.节流
       高频事件触发，但在n秒内只会执行一次，所以节流会稀释函数的执行频率
  
  延伸知识：https://www.bilibili.com/video/BV1nb411P7tQ?p=13
           闭包