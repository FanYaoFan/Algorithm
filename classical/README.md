#  经典排序算法
return 下面的代码就不再执行
```JavaScript
let sum = (n,m) =>{
    let total = null
    total = n + m
    return total 
    console.log(1) // 不执行
}
```
要用到的数组api(push,pop,unshift,splice,concat,slice)
## 1 冒泡排序(bubble)
拿数组的当前项与后一项比较,最大的排在后面(每一轮是否可以得出一个最大值?可以),如果当前项比后一项大,则两项交换位置(让大的靠后)
每一轮完成后,都会得出一个最大值(放在末尾)  
次轮不需要跟最末尾比较
两者交换, i = 1 , 是将1赋值给a,也就是说等号右边赋值给等号左边  
```JavaScript
let temp = [], //两种饮料互换瓶子理解
 ary[i] = temp // arr[i]被赋值为空
 temp = ary[i] // 如是才被赋值为i的值
 现在ary[i]为空, 所以  ary[i] = ary[j] // 而不是ary[j] = ary[i]
 现在ary[j]为空,但temp存储的是i的值,所以,arr[j]=temp
```
```JavaScript
function bublle(ary) {
    let temp = null
    for (let i = 0; i < ary.length - 1; i++) {
      for (let j = 0; i < ary.length - i; j++) {
        if (arr[j] > arr[j + 1]) {
          temp = ary[j]
          ary[j] = ary[j + 1]
          ary[j + 1] = temp
        }
      }
    }
    return ary
  }
  console.log(ary)
```

## 2 插入排序(insert)
以抓牌理牌为理解  
1. 先假设抓牌(设置一个空数组),然后把要排序的数组的第一项(ary[0])放到这个数组中
2. 在依次抓台面上的牌,注意从第二张牌开始(for let i = 0; i < ary.length;i++)
3. 从台面上抓一张牌(let A = ary[i])
4. 与你手上的牌比较,从后往前比(更好理解)(for let j = handle.length -1; j--)
5. 从handle(手上的最后一张)开始比 (let B = handle[j])
6. 如果抓的牌>手上最右边(最大的牌)就插入到最后splice(),如果是倒数第j张,则要插入到j的后面,即handle.splice(j+1,0,A)为什么是j+1,是因为splice的语法,新增到当前项的后面,要在当前索引下新增,就要索引+1,才能实现;
7. 如果A比到第一项了,即j===0,就放在最前边unshfit()  

```JavaScript
function insert(ary) {
        //  1  把handle看做手,先抓第一张牌放到手里
        let handle = []
        handle.push(ary[0])
        // 2 依次把台面上的牌抓完 (从第二张开始)
        for (let i = 1; i < ary.length; i++) {
            let A = ary[i]
            // 3 把抓来的每张牌都和手上的牌做比较(从后往前做比较)
            for (let j = handle.length - 1; j >= 0; j--) {
                let B = handle[j]
                if (A > B) {
                    handle.splice(j + 1, 0, A)
                    break
                }
                // 4 比到第一项了,就直接插在数组最前面
                if (j === 0) {
                    handle.unshift(A)
                }
            }
        }
        return handle
    }
    console.log(insert(ary))
```
## 3 递归(recursion)
函数执行的时候,自己调用自己
``` JavaScript
function fn(){
   fn()
}
这种递归会导致栈溢出
```
## 4 快速排序(quick)
```JavaScript

 function Quick(ary) {
        if (ary.length <= 1) {
            return ary
        }

        //    1.首先获取数组中间的index值
        let middleIndex = Math.floor(ary.length / 2)
        //   2. 根据index值得到数组中间值 (splice删除返回值是删除的数组(此处是当前值))
        let middleValue = ary.splice(middleIndex, 1)[0]
        console.log(middleValue)
        // 3. 准备左右两个空数组,循环ary剩下的每一个数与中间这项比较,小的就放在左边这个数组,
        // 大的就放在右边
        let aryLeft = [],
            aryRight = []
        for (let i = 0; i < ary.length; i++) {
            let item = ary[i]
            item > middleValue ? aryRight.push(item) : aryLeft.push(item)
            // if(ary[i]<minddleValue){
            //     aryLeft.push(ary[i])
            // }else if(arr[i]>minddleValue){
            //     aryRight.push[i]
            // }
        }
        // 采用递归,来让左右两边的数组以相同方式(即找到中间项,然后将剩下的数与中间项比较,小为左,大为右,直至全部完成)
        return Quick(aryLeft).concat(middleValue, Quick(aryRight))
    }
      let ary = [12,8,5,16,1,24]
    console.log(Quick(ary))

```