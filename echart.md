1. Option 的理解
1.1 Option 是对象还是什么数组？
    Option 是对象


2. 怎么在小程序中用echarts及局部更新

2.1 wxml 中引入组件。

2.2 创建initChart函数初始话echarts组件

2.3 局部属性更新

echarts 局部刷新
在 ECharts 中，如果你想要进行局部刷新，你可以使用 setOption 方法来更新图表的某一部分，而不是重新初始化整个图表。这样可以节省资源并提高性能。

以下是一个简单的例子，展示了如何使用 setOption 来更新 ECharts 图表的一个系列（Series）数据：


        // 假设你已经有一个初始化好的 echarts 实例
        var myChart = echarts.init(document.getElementById('main'));
         
        // 图表的初始选项
        var option = {
            xAxis: {
                type: 'category',
                data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
            },
            yAxis: {
                type: 'value'
            },
            series: [{
                data: [120, 200, 150, 80, 70, 110, 130],
                type: 'bar'
            }]
        };
         
        // 使用初始选项初始化图表
        myChart.setOption(option);
         
        // 局部刷新数据的函数
        function updateSeriesData(newData) {
            // 使用 setOption 更新系列数据
            myChart.setOption({
                series: [{
                    data: newData
                }]
            });
        }
         
        // 假设我们要更新的新数据
        var newData = [180, 240, 300, 100, 90, 230, 210];
         
        // 调用函数更新图表数据
        updateSeriesData(newData);
    


2.3 当一个页面中有动态个图时，怎么动态局部更新？
难点： 因为每一个图初始化后，如果需要局部更新，就需要在对应实例对象上调用setOption。

尝试办法：
2.3.1 在page里面保留一个map 对象。 然后保存相应创建的对象实例。 
    // 创建一个Map对象
    const map = new Map();
     
    // 创建两个对象
    const obj1 = { key: 'one', value: 1 };
    const obj2 = { key: 'two', value: 2 };
     
    // 将对象作为值添加到Map中
    map.set(obj1.key, obj1);
    map.set(obj2.key, obj2);
     
    // 获取Map中的对象
    console.log(map.get('one')); // 输出：{ key: 'one', value: 1 }
    console.log(map.get('two')); // 输出：{ key: 'two', value: 2 }

2.3.2 这个map 设置在哪里呢？ data之下，还是和data并列？