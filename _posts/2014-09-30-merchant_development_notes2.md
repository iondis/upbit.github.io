---
layout: post
title: TravelingMerchant开发手记02 - 供给与需求模型
description: "Traveling Merchant Development Notes 02"
category: game
comments: true
share: true
---

说到商业模拟，我们往往想到的是大航海时代里，在两个港口来回倒卖特产的情景，然而现实中的经济远非这么简单。例如小麦，它的价格由当地的供给与需求决定，如果供不应求势必会导致价格的上涨，而供过于求则会致使小麦价格的下跌。小麦同时又是面粉的原料(投入品)，其价格直接影响面粉的价格；并且小麦还有大麦、黑麦、燕麦等代替品，当小麦价格过高时，人们又会选择相对低廉的代替品，从而导致需求的二次变化...

对于一个经济概念还仅仅停留在大学时背诵的“生产力决定生产关系”的门外汉，直接上来就思考供需理论实在是难度太大了点。好在现在是个网络的时代，搜了本曼昆的[《经济学原理》](http://book.douban.com/subject/3719533/)猛啃，算是摸到了点门道。

首先要明确的是，**价格影响供给与需求**。以白菜为例，如果价格涨到50块钱一斤，想必商家会想方设法从附近省市调货，甚至把自家地下室里储藏过冬的白菜都拿出来卖了；如果白菜跌到5毛钱3斤，老百姓是高兴了但想必种白菜的没人愿意拿出来卖，还不如留着自家煮火锅来的合算。

所以物品的价格，会趋于一个稳定点，即[供给与需求曲线](http://zh.wikipedia.org/wiki/%E4%BE%9B%E7%BB%99%E5%92%8C%E9%9C%80%E6%B1%82)的交点，并且在这一点对应的价格P，使得供给与需求刚好都等于Q：

<center>![供需平衡价格]({{ site.url }}/images/Supply-demand-equilibrium.svg.png)</center>

图中需求曲线(红色)和供给曲线(蓝色)，存在不同的曲率以及与坐标轴的交点。交点可以理解为最大需求量(价格为0时)以及最小供给价格(供给为0时)，而曲率则比较复杂，还需要从影响供需的因素说起。

首先来考虑**影响需求的因素**，在游戏中存在以下几个方面：

1. **收入：**购买者的收入决定了购买力，并且当收入过低时，低档商品的需求相反会得到提升；
 - <span style="color:#888;">因为低档商品与正常商品的模型完全不同，这里只考虑随着收入变化而同步变化的正常商品。同时区域的收入也可以抽象为该区域的繁荣度。</span>
2. **相关物品价格：**就像开头提到的小麦，它存在其他谷物的代替品，在小麦价格上涨时其自身需求下降，并且其他代替品的需求上升；同样的还有互补品，比如面包卖的好时，店里的咖啡或饮料销量同时会得到提升；
3. **嗜好：**比如中国北方喜食面食，而南方则以大米为主，这是由于地域差异决定的；
4. **预期：**如果某个商品的价格即将上涨，那么购买的人会在段时间内暴增，相反下跌前需求会急剧减少；
 - <span style="color:#888;">不过预期刻画的是短期内的变化，不会长时间影响需求量，所以暂时可以不考虑这个因素。</span>

这些因素共同决定了物品的需求变化(需求弹性)。相对应的，**供给**也同样存在以下几种**影响因素**：

1. **投入品价格：**原料等价格上涨，在市场价不变时会导致供给量下降(利润变低了)；
2. **技术：**例如小麦的种植技术改进，使单位面积的小麦产量翻倍。在那么同样售价下，市场的供给也得到了近乎翻倍的提升；
3. **预期：**不仅仅消费者，供应商也会有预期。

因为模拟的是欧洲中世纪的贸易，大多都是手工或作坊生产，这里忽略生产成本对供给的影响。

说了这么多理论，再回头看下 规则3 [**供需与价格**：区域中的物品进货价格，由区域的供需关系决定] 这条，物品的均衡价格正好用供需曲线来刻画：

<center>![供给和需求]({{ site.url }}/images/Supply-demand-right-shift-demand_zh-tw.svg.png)</center>

当区域中代替品价格上涨时，小麦的需求曲线从D1变化到D2，及相同价格P1下需求量上升。而由于供给曲线S未变，均衡价格从P1慢慢变化到P2(因为持续供不应求)，直到达到新的均衡点(Q2,P2)为止。这个过程就是当某种谷物(比如大麦)价格上涨时，小麦价格与供需的变化过程。

不过，光有这些理论还远远达不到构筑模型的程度，[TravelingMerchant开发手记03](#)将继续阐述商人、供应商的模拟，来构筑供需平衡的市场规律。
