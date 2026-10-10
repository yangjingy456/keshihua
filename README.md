# 01_book_purchase
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams["font.sans-serif"] = ["SimHei"]
plt.rcParams["axes.unicode_minus"] = False
x = np.arange(5)
y1 = [1200, 2400, 1800, 2200, 1600]
y2 = [1050, 2100, 1300, 1600, 1340]
bar_width = 0.6
tick_label = ["家庭", "小说", "心理", "科技", "儿童"]
fig = plt.figure()
ax = fig.add_subplot(111)
# 绘制柱形图 , 并使用颜色
ax.bar(x, y1, bar_width, color="#FFCC00", align="center", label ="地区1")
ax.bar(x, y2, bar_width, bottom=y1, color="#B0C4DE", align="center", label="地区2")
ax.set_ylabel("采购数量(本)")
ax.set_xlabel("图书种类")
ax.set_title(" 地区1和地区2对各类图书的采e购情况")
ax.grid(True, axis='y', color="gray", alpha=0.2)
ax.set_xticks(x)
ax.set_xticklabels(tick_label)
ax.legend()
plt.show()



# 02_dollar_RMB_exchange_rate
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams["font.sans-serif"] = ["SimHei"]
plt.rcParams["axes.unicode_minus"] = False
# 汇率
eurcny_2017 = np.array([6.8007, 6.8007, 6.8015, 6.8015, 6.8060,  6.8060, 6.8060, 6.8036, 
                        6.8025, 6.7877, 6.7835, 6.7758, 6.7700, 6.7463, 6.7519,6.7511, 
                        6.7511, 6.7539, 6.7265])
eurcny_2019 = np.array([6.8640, 6.8705, 6.8697, 6.8697, 6.8697,6.8881, 6.8853, 6.8856, 
                        6.8677, 6.8662, 6.8662, 6.8662, 6.8827, 6.8761, 6.8635,6.8860, 
                        6.8737, 6.8796, 6.8841])
date_x = np.array([3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 17, 18, 19, 24, 25, 26, 31])
fig = plt.figure()
ax = fig.add_subplot(111)
# 第1 条折线 : 湖绿色 , 实线 , 线宽为 2
ax.plot(date_x, eurcny_2017, color='#006374', linewidth=2, label='2017年7月美元/人民币汇率')
# 第2 条折线 : 紫色 , 长虚线 , 线宽为 2
ax.plot(date_x, eurcny_2019, color='#8a2e76', linestyle='--', linewidth=2, label='2019年7月美元/人民币汇率')
ax.set_title('2017年7月与2019年7月美元/人民币汇率走势')
ax.set_xlabel('日期')
ax.set_ylabel('汇率')
ax.legend()
plt.show()



# 03_sales_of_different_products
import numpy as np
import matplotlib.pyplot as plt
plt.rcParams["font.sans-serif"] = ["SimHei"]
plt.rcParams["axes.unicode_minus"] = False
sale_a = [2144, 4617, 7674, 6666]
sale_b = [853, 1214, 2414, 4409]
sale_c = [153, 155, 292, 680]
fig = plt.figure()
ax = fig.add_subplot(111)
# 绘制具有不同线条样式的折线图
ax.plot(sale_a, 'D-', sale_b, '^:', sale_c, 's--')
ax.grid(alpha=0.3)
ax.set_ylabel('销售额(万元)')
ax.set_xticks(np.arange(len(sale_c)))
ax.set_xticklabels(['第1季度','第2季度', '第3季度', '第4季度'])
ax.legend(['产品A','产品B','产品C'])
plt.show()



# 04_maximum_minimum_temperatures
import matplotlib.pyplot as plt
import numpy as np
plt.rcParams['font.sans-serif'] = ['SimHei']
plt.rcParams['axes.unicode_minus'] = False
x = np.arange(4, 19)
y_max =[32, 33, 34, 34, 33, 31, 30, 29, 30, 29, 26, 23, 21, 25,  31]
y_min = [19, 19, 20, 22, 22, 21, 22, 16, 18, 18, 17, 14, 15, 16 , 16]
# 可以调用多次plot() 函数
plt.plot(x, y_max, marker='o', label='最高温度')
plt.plot(x, y_min, marker='o', label='最低温度')
# 为图表添加注释并设置字体的样式
x_temp = 4
for y_h, y_l in zip(y_max, y_min):
    plt.text(x_temp-0.3, y_h  + 0.7, y_h, family='SimHei', fontsize=8, fontstyle='normal')
    plt.text(x_temp-0.3, y_l  + 0.7, y_l, family='SimHei', fontsize=8, fontstyle='normal')
    x_temp  += 1
plt.title('未来15天最高气温和最低气温的走势')
plt.xlabel('日期')
plt.ylabel('温度($^\circ$C)')
plt.ylim(0, 40)
plt.legend()
plt.show()


# 05_colorful_snowflakes
import numpy as np
import matplotlib.pyplot as plt
def koch_snowflake(order, scale=10):
    def _koch_snowflake_complex(order):
        if order == 0:
            # 初始三角形
            angles = np.array([0, 120, 240]) + 90
            return scale / np.sqrt(3) * np.exp(np.deg2rad(angles)  * 1j)
        else:
            ZR = 0.5 - 0.5j  * np.sqrt(3) / 3
            p1 = _koch_snowflake_complex(order - 1)  # 起点
            p2 = np.roll(p1, shift=-1)               # 终点
            dp = p2 - p1                             # 连接向量
            new_points = np.empty(len(p1) * 4, dtype=np.complex128)
            new_points[::4] = p1
            new_points[1::4] = p1 + dp / 3
            new_points[2::4] = p1 + dp * ZR
            new_points[3::4] = p1 + dp / 3 * 2
            return new_points
    points = _koch_snowflake_complex(order)
    x, y = points.real, points.imag
    return x, y
x, y = koch_snowflake(order=2)
fig = plt.figure()
ax = fig.add_subplot(111)
ax.fill(x, y, facecolor='lightsalmon', edgecolor='orangered', linewidth=3)
plt.show()
