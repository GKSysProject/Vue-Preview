# APIs

## `/api/year`

接受一个参数`y`，为年份，范围2020-2024
返回格式：

```
{
    xAxis: xAxis,
    series: series
}
```

## `/my`

返回格式：

```
{
    name: name,
    score: score,
    rank: rank,
    schoolList: []
}
```

## `/api/universities`

返回各省大学数量

```
{
    '北京': 91,
    '上海': 64,
    '天津': 55,
    '重庆': 30,
    '河北': 45,
    '山西': 35,
    '内蒙古': 25,
    '辽宁': 50,
    '吉林': 40,
    '黑龙江': 38,
    '江苏': 70,
    '浙江': 60,
    '安徽': 48,
    '福建': 42,
    '江西': 36,
    '山东': 65,
    '河南': 58,
    '湖北': 52,
    '湖南': 47,
    '广东': 75,
    '广西': 33,
    '海南': 20,
    '四川': 68,
    '贵州': 28,
    '云南': 32,
    '西藏': 10,
    '陕西': 54,
    '甘肃': 26,
    '青海': 15,
    '宁夏': 18,
    '新疆': 22
}
```

## `/api/university-details`

接受参数`name`

返回大学信息数据，例如

```
{
    name: "示例大学",
    logo: "path/to/logo.png",
    description: "这是一个示例大学的简介。",
    majors: [
        { name: "计算机科学", admissionScore: 600 },
        { name: "电子工程", admissionScore: 580 }
    ]
}
```

## `/search`

接受参数`q`

返回搜索结果列表

```
["北京大学","东北大学"]
```

## `/geodata`

返回中国地图地理数据（可能打算使用别的）

## `/api/topunis`

返回搜索量排名前十的院校名称列表