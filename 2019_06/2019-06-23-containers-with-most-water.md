####题目： 给定n个非负整数a1，a2，...，an，其中每个表示坐标（i，ai）处的点。 绘制n条垂直线，使得线i的两个端点位于（i，ai）和（i，0）。 找到两条线，它们与x轴一起形成一个容器，使其含有最多的水。
####例如： [1,8,6,2,5,4,8,3,7]， 返回49（第二位的8，最后的7）
####思路：我们需要确定容器两端的线，将初始值设为数组的开始和结束，这样容器宽度最宽。当宽度确定时想让容器的装水变多，只能让高度变高，而决定容器高度的是矮的那一边，所以那边比较矮就更新那边的值。在遍历过程中更新max值。
代码
```
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function(height) {
    var max = 0,
        left = 0,
        rigth = height.length - 1;
    while(left < rigth) {
        max = Math.max(max, (rigth - left) * Math.min(height[left], height[rigth]));
        if(height[left] < height[rigth]) {
            left++;
        } else {
            rigth--;
        }
    }
    return max;
};
```