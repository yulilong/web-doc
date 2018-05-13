## 冒泡排序

算法描述：

1. 比较相邻的元素。如果第一个比第二个大，就交换它们两个；
2. 对每一对相邻元素作同样的工作，从开始第一对到结尾的最后一对，这样在最后的元素应该会是最大的数；
3. 针对所有的元素重复以上的步骤，除了最后一个；
4. 重复步骤1~3，直到排序完成。

```javascript
function sort(arr) {
  var ar = []; var tmp;
  for (var i = 0; i < arr.length; i++) {
    for (var j = 0; j < arr.length - 1 - i; j++) {
      if (arr[j] > arr[j + 1]) {
        tmp = arr[j]; arr[j] = arr[j + 1]; arr[j + 1] = tmp;
      }
    }
  }
  console.log(arr)
}
sort([3, 9, 2])
```







十大经典排序算法：

https://www.cnblogs.com/onepixel/articles/7674659.html

https://www.cnblogs.com/beli/p/6297741.html

https://www.cnblogs.com/liyongshuai/p/7197962.html