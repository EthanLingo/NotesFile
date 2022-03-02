最简单的TD方法称为**TD(0)**方法。估计目标为

$$
V\left(S_{t}\right) \leftarrow V\left(S_{t}\right)+\alpha\left[R_{t+1}+\gamma V\left(S_{t+1}\right)-V\left(S_{t}\right)\right]
$$

相比之下，一个适用于非平稳环境之简单的每次访问型蒙特卡罗方法估计目标为：

$$
V\left(S_{t}\right) \leftarrow V\left(S_{t}\right)+\alpha\left[G_{t}-V\left(S_{t}\right)\right]
$$


#算法 TD(0)算法：

![[Pasted image 20211209214135.png]]

回溯图：

![[Pasted image 20211209214248.png]]

蒙特卡罗误差可以写成TD误差之和。
