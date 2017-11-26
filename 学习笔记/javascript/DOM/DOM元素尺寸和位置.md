

## offset家族 ##

**offsetWidth和offsetHeight**：可以获取元素实际大小（width+padding+border）。
可以获取元素的大小，但是不能设置。

    box.offsetWidth;
    box.offsetHeight;

**offsetTop和offsetLeft**：
可以获取当前元素相对于父元素的位置。

    box.offsetLeft;
    box.offsetHeight;

PS:如果父盒子中没有设置相对定位的，那么元素就相对于窗口定边的距离


## scroll家族 ##
**scrollWidth和scrollHeight**：
可以获取滚动内容的元素大小

    box.scrollWidth;
    box.scrollHeight;

**scrollTop和scrollLeft**：
获取页面被滚动条卷去的高度和左侧的宽度

    box.scrollTop;
    box.scrollLeft;


## client家族 ##
**clientWidth和clientHeight**：
这组属性可以获取元素可视区的大小，可以得到元素内容及内边距所占据的空间大小。（width+padding）

    box.clientWidth;
    box.clientHeight;

**clientLeft和clientTop**(完全没用)：
就是borderTop与borderLeft

----------


####三个家族的区别 ####




- offset家族用来获取**元素自身**的大小和位置
- scroll家族用来获取 **元素内容**的大小和位置
- client(客户区、可视区)家族用来获取**元素可视区域**的大小


----------

- 偏移offsetWidth: width + padding + border
- 卷曲scrollWidth: width + padding  不含border
- 可视clientWidth: width + padding  不包含border



> **如果内容没有超出盒子范围：clientWidth与scrollWidth相同**






