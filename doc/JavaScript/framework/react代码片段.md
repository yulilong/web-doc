[TOC]

### 1. setState异步执行，中立即使用的方法

```jsx
this.setState({
    businessLine: [{name: '-'},...res.data.data],
},()=>{
    // 这里可以立即使用
});
```

### 2. jsx中HTML三木运算

```jsx
{this.state.businessLine ? (
    this.state.businessLine.map((item, i) => (
        <Option key={i.toString()} value={item.id}>{item.name}</Option>
    ))
) : (
    <Option key='1' value=''></Option>
)}
```

### 3. 根据不同条件拼接字符串，用于类样式名字拼接

```jsx
/**
 * 拼接字符串，用于把符合条件的类样式名字拼接在一起
 * @param  {Object} obj     样式名字和是否符合条件
 * @return {String}         计算后的样式名字 字符串
*/
setClassNames = (obj) => {
  if ( typeof obj !== 'object') {
    return '';
  }
  let key;
  let str = '';
  for (key in obj) {
    if(obj[key]) {
      str += ' ' + key;
    }
  }
  return str;
}
return (
<span
   className={this.setClassNames({
       'active': this.state[e.key] === item.value,
       'forbidden': this.state.dimensional === e.value,
   })}
>{item.name}</span>
)
```

