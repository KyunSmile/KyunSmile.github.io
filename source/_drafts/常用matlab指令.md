常用matlab函数



# 矩阵操作

**矩阵合并：**cat(dim,A,B)



# 数据读取

## 单文件

**csv读取：**M = csvread('filename') 

## 批量

* 要读入的文件下的文件名称依序列的方式命名，如a1b.mat, a2b.mat,...

    ```matlab
    filepath='';%文件夹的路径
    for i=1:n %n是要读入的文件的个数
        load（[filepath 'a' num2str(i) 'b' '.mat']）
    end
    ```

* 非规则命名

  * 先得到文件路径

    ```matlab
    di = dir('文件路径*.jpg')；
    ```

  * 读入

    ```matlab
    for k= 1:length（di）
    	I(k,:,:) = imread(['文件路径',di(k).name]); 
    end 
    ```

# 画图

**坐标范围：**axis([xmin xmax ymin ymax]); 

**图例：**legend('line 1','line 2'); 