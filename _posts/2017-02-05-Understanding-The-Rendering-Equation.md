An important step towards photo-immersive virtual reality (or computer generated photo-realistic renderings that our visual system can be duped and tricked easily to believe that it is real) is to be able to approximate the light transport happening in the real world. Real world is very chaotic and various complicated phenomena happen as photons travel from one medium to another in space. Obviously, our visual system is not capable of sampling the world at anything beyond 60Hz and therefore, we can never see in reality how photons move around, bounce off and interact with each other. However, given simple laws of optics, we can write down the light transport equation to a sufficient degree of accuracy that allows us to create a faithful representation of real world via ray tracing on a computer. The classic rendering equation lies at the heart of all ray tracers except that each one uses a different way to approximate and solve the equation. In its simplest form, the rendering equation is the following

$$L_o(x, \omega_r) =  L_{e}(x, \omega_r) + L_i(x, \omega_i) f(x, \omega_i, \omega_r) (\omega_i \cdot n)$$
 
 Light leaving a surface at position $x$ in a direction $\omega_r$ is a sum of light emitted from the surface in that direction (most surfaces do not emit so this is generally zero except for light sources) and the incoming light from direction $\omega_i$ reflected in that direction, where $L_i$ is a incoming light intensity, $f(\cdot)$ is the surface BRDF which encodes the fraction of incoming light that is reflected from the surface as some of the light is absorbed by the surface,  $(\omega_i \cdot n)$ is the attenuation of the light and $n$ is the normal of the surface. If there are multiple light sources, one can simply sum the incident light from these sources in the equation and arrive at the following expression

$$L_o(x, \omega_r) = L_{e}(x, \omega_r) + \sum L_i(x, \omega_i) f(x, \omega_i, \omega_r) (\omega_i \cdot n)$$

However, an important assumption underpinning this equation is that $L_i$ is coming directly from a  light source. Therefore, this doesn't take into account various other sources of incoming light *i.e.* indirect light from a other surfaces falling at a point $x$. Indirect light is the light that reaches a surface after bouncing off from another. Therefore, if we consider the hemispherical volume around a point $x$ and integrate the incoming light from all directions, we obtain

$$L_o(x, \omega_r) = {L_{e}(x, \omega_r)} + \int_{\Omega} L_i(x, \omega_i) f(x, \omega_i, \omega_r) (\omega_i \cdot n) d \omega_{i}$$

![Alt Text](/images/rendering.png) 

Interestingly incident light at point $x$ from a direction $\omega_i$ is nothing but the reflected light $L_o$ from a point $\hat{x}$ in the direction $-\omega_i$. Therefore, the equation simplifies to 

$$L_o(x, \omega_r) = L_{e}(x, \omega_r) + \int_{\Omega} L_o(\hat{x}, -\omega_i) f(x, \omega_i, \omega_r) (\omega_i \cdot n) d \omega_{i}$$

where $\hat{x}$ is obtained by casting a ray from the position $x$ in the direction $-\omega_i$ *i.e.* $\hat{x}$ is the first surface point a ray hits when traversed back from $x$ in the direction $-\omega_i$. Therefore, at each point, the outgoing light in one direction is the inegral of incoming light from all directions multiplied by the surface reflectance property. This structure of the equation resembles the Fredholm integral of the form 

$$l(u) = e(u) + \int l(v) K(u,v) dv$$

Discretising the hemispherical volume allows us to approximate this equation further and implement that on a computer. 

$$L_{o,j} = L_{e,j} + \sum_{i} L_{o,i} F_{i,j}$$ 

and this leads to the following matrix form

$$\begin{pmatrix}
1-F_{1,1} & -F_{1,2} & \dots & -F_{1,n}\\ 
-F_{2,1}  & 1-F_{2,2}  & \dots  & -F_{2,n} \\
\vdots & \vdots & \dots & \vdots \\
-F_{n,1} & -F_{n,2} & \dots & 1-F_{n,n} \\ 
\end{pmatrix}
 \begin{pmatrix} 
 L_{o,1} \\ 
L_{o,2} \\
\vdots \\
L_{o,n} \\
\end{pmatrix} = \begin{pmatrix} 
 L_{e,1} \\ 
L_{e,2} \\
\vdots \\
L_{e,n} \\
\end{pmatrix}$$

This further simplifies to 

$$\begin{pmatrix} 
 L_{o,1} \\ 
L_{o,2} \\
\vdots \\
L_{o,n} \\
\end{pmatrix} = \begin{pmatrix} 
 L_{e,1} \\ 
L_{e,2} \\
\vdots \\
L_{e,n} \\
\end{pmatrix} + \begin{pmatrix}
F_{1,1} & F_{1,2} & \dots & F_{1,n}\\ 
F_{2,1}  & F_{2,2}  & \dots  & F_{2,n} \\
\vdots & \vdots & \dots & \vdots \\
F_{n,1} & F_{n,2} & \dots & F_{n,n} \\ 
\end{pmatrix}
 \begin{pmatrix} 
L_{o,1} \\ 
L_{o,2} \\
\vdots \\
L_{o,n} \\
\end{pmatrix}$$

Such equations often appear in standard inverse problems in computer vision and are solved via jacobi iteration recurrence of the form 

$$L_{o}^{k} = L_{e} + F L_{o}^{k-1}$$

where $k$ denotes the iteration number. One may be able to also derive similar expression using binomial theorem *i.e.*

$$(I - F)L_{o} = L_{e} \\
L_{o} = (I - F)^{-1}L_{e} \\
L_{o} = (I + F + F^{2} + F^{3}...) L_{e}\\
$$


In the following, we see four iterations of this recurrence and also how each iteration creates a more visually appealing image. 

<img src="/images/L_e.png" width="150">
<img src="/images/L_epKL_e.png" width="150">
<img src="/images/L_epKL_epK2L_e.png" width="150">
<img src="/images/L_epKL_epK2L_epK3L_e.png" width="150">

In the first iteration, we see there is no outgoing light from any surface and only light source emits the light as a result it is very bright. However, this light then propagates across the surfaces and the floor and walls start to accumulate the color while ceiling still looks black because there is no transport of light from other surfaces to ceiling yet. In the next two iterations we see that the ceiling starts to accumulate the colour as well and we know now that the light transport is happening from every surface to every other surface.
