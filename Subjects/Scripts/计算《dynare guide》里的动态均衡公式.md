# 计算《dynare guide》里的动态均衡公式



列出原始公式：
$$
{\rm family.u} = \max  E_t \sum_{t=0}^{\infty}{\beta^{t} \left(\log[c_t]-\theta \frac{h_t^{1+\psi}}{1+\psi} \right)}
\tag{1}
$$

$$
c_t+i_t=y_t \tag{2}
$$

$$
k_{t+1}=\exp[b_t] i_t + (1-\delta) k_t \tag{3}
$$

$$
y_t=\exp[a_t]k_t^{\alpha}h_t^{1-\alpha} \tag{4}
$$

。其中，公式(3)可以变形为(5)
$$
i_t=\frac{k_{t+1}-(1-\delta) k_t}{\exp[b_t]} \tag{5}
$$
。构建家庭效用最大化的拉格朗日函数，其中代入$i_t,y_t$得(6)：
$$
E_t \sum_{t=0}^{\infty}{\beta^{t} \left(\log[c_t]-\theta \frac{h_t^{1+\psi}}{1+\psi} - 
\lambda_t \left( c_t + \frac{k_{t+1}-(1-\delta) k_t}{\exp[b_t]} - \exp[a_t]k_t^{\alpha}h_t^{1-\alpha}
\right) \right)
}
\tag{6}
$$
。

求一阶条件(6)可得(7)(8)(9)：
$$
\begin{align}
& \frac{\partial \rm family.u}{\partial c_t} = 0 \\
\Leftrightarrow & \frac{1}{c_t}-\lambda_t=0 \\
\end{align}
\tag{7}
$$

$$
\begin{align}
& \frac{\partial \rm family.u}{\partial h_t} = 0 \\
\Leftrightarrow & -\theta h_t^\psi - \lambda_t (1-\alpha) \left( -\exp[a_t] k_t^\alpha h_t^{-\alpha} \right) =0 \\
\end{align}
\tag{8}
$$

$$
\begin{align}
& \frac{\partial \rm family.u}{\partial k_t} = 0 \\
\Leftrightarrow & -E_t\left[
\beta^t \lambda_t \left(
\frac{-(1-\delta)}{\exp[b_t]}-h_t^{1-\alpha} \exp[a_t] k_t^{\alpha-1}
\right)
\right] 
-E_{t-1}\left[
\beta^{t-1} \lambda_{t-1} \left(
\frac{1}{\exp[b_{t-1}]}
\right)
\right] \\
代入(7)得 \Leftrightarrow & \beta E_t\left[
\left(
\frac{c_{t-1} \exp[b_{t-1}]}{c_{t} \exp[b_{t}]}
\right)
\cdot
\left(
(1-\delta)-\exp[b_t] h_t^{1-\alpha} \exp[a_t] k_t^{\alpha-1}
\right)
\right]
=1 \\
代入(4)得 \Leftrightarrow & \beta E_t\left[
\left(
\frac{c_{t-1} \exp[b_{t-1}]}{c_{t} \exp[b_{t}]}
\right)
\cdot
\left(
(1-\delta)- \exp[a_t] y_t
\right)
\right]=1
\end{align}
\tag{9}
$$





