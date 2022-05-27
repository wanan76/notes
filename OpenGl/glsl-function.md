## GLSL内建函数
### 角度和三角函数
##### genType radians(genType degrees)
``` glsl
float d = 90.0;
float r = radians(d); 
```
##### genType degrees(genType radians)
``` glsl
float r = 3.14;
float d = degrees(r);
```
##### genType sin(genType angle)
``` glsl
float pi = 3.14;
sin(-pi); // result = 0.0
sin(-pi / 2.0); // result = -1.0
sin(0.0); // result = 0.0
sin(pi / 2.0); // result = 1.0
sin(pi); // result = 0.0
```
##### genType cos(genType angle)
``` glsl
float pi = 3.14;
cos(-pi); // result = -1.0
sin(-pi / 2.0); // result = 0.0
sin(0); // result = 1.0
sin(pi / 2.0); // result = 0.0
sin(pi); // result = -1.0
```
##### genType tan(genType angle)
##### genType asin(genType angle)
##### genType acos(genType angle)
##### genType atan(genType angle)
---
### 指数函数
##### genType pow(genType x, genType y)
``` glsl
// 结果为x的y次方
int x = 5;
int y = 3
int result = pow(x, y); // 5的3次方
```
##### genType exp(genType x)
``` glsl
/* 
exp(x) 等价于 e的x次方
这里的e是数学常数，就是自然对数的底数，近似等于 2.718281828，还称为欧拉数
*/
float x = 5.0;
float result = exp(x); // e的5次方
```
##### genType log(genType x)
``` glsl
/* 
exp(x) 函数的反函数
float y = log(x) 等价于 float x = exp(y)
如果x小于等于0，结果是未定义的。
*/
```
##### genType exp2(genType x)
``` glsl
/* 
exp2(x) 等价于 2的x次方
*/
float x = 5.0;
float result = exp2(x); // 2的5次方
```
##### genType log2(genType x)
``` glsl
/* 
exp2(x) 函数的反函数
float y = log2(x) 等价于 float x = exp2(y)
如果x小于等于0，结果是未定义的。
*/
```
##### genType sqrt(genType x)
``` glsl
// x的平方根
// 如果x小于等于0，结果是未定义的。
float result = sqrt(4.0); // result = 2.0
```
##### genType inversesqrt(genType x)
``` glsl
// 1 除以 x的平方根
// 如果x小于等于0，结果是未定义的。
float result = inversesqrt(4.0); // result = 1.0 / 2.0
```
---
### 常用函数
##### genType abs(genType x)
``` glsl
// 取x的绝对值
float result = abs(-1.0); // result = 1.0;
```
##### genType sign(genType x)
``` glsl
// 取x的符合
// 如果 x > 0.0, 返回1.0
// 如果 x = 0.0, 返回0.0
// 如果 x < 0.0, 返回-1.0
```
##### genType floor(genType x)
``` glsl
// 舍去法
floor(2.3); // 2.0
floor(2.5); // 2.0
floor(2.8); // 2.0
```
##### genType ceil(genType x)
``` glsl
// 进一法
ceil(2.0); // 2.0
ceil(2.3); // 3.0
ceil(2.5); // 3.0
ceil(2.8); // 3.0
```
##### genType fract(genType x)
``` glsl
// 取小数部分
fract(2.0); // 0.0
fract(2.3); // 0.3
fract(2.5); // 0.5
fract(2.8); // 0.8
```
##### genType mod(genType x, genType y)
``` glsl
// 模运算
mod(3, 2); // 1
```
##### genType min(genType x, genType y)
``` glsl
// 取x，y最小值
min(3, 2); // 2
```
##### genType max(genType x, genType y)
``` glsl
// 取x，y最大值
max(3, 2); // 3
```
##### genType clamp(genType x, genType minVal, genType maxVal)
``` glsl
// 如果x < minVal, 取minVal
// 如果x > maxVal, 取maxVal
// 如果minVal <= x <= maxVal, x
clamp(1, 2, 5); // 2
clamp(6, 2, 5); // 5
clamp(3, 2, 5); // 3
```
##### genType mix(genType x, genType y, genType a)
``` glsl
// 等价于 x * (1 - a) + y * a
```
##### genType step(genType edge, genType x)
``` glsl
// 如果 x < edge, 返回0.0
// 如果 x >= edge, 返回1.0
step(2.0, 1.0); // 0.0
step(2.0, 3.0): // 1.0
```
##### genType smoothstep(genType edge0, genType edge0, genType x)
``` glsl
// edge1 必须大于 edge0
// 如果 x <= edge0, 返回0.0
// 如果 x >= edge1, 返回1.0
// 等价于
float function() {
    float t;
    t = clamp((x - edge0) / (edge1 - edge0), 0, 1);
    return t * t * (3 - 2 * t);
}
```
---
### 几何函数
##### float length(genType x)
``` glsl
// 返回向量长度
```
##### float distance(genType p0, genType p1)
``` glsl
// 返回向量p0 p1之间的距离
// 等价于 length(p0 - p1)
```
##### float dot(genType x, genType y)
``` glsl
// 点乘
// 返回向量y在向量x上的垂直投影长度
// 结果为 x[0] * y[0] + x[1] * y[1] + ...
vec3 x = vec3(3.0, 3.0, 3.0);
vec3 y = vec3(0.0, 5.0, 1.0);
float lx = length(x);
float ly = lenght(y);
float rcos = dot(x, y) / (lx * ly);
```
##### vec3 dot(vec3 x, vec3 y)
``` glsl
// 叉乘
// 返回向量x和y的法线向量，长度为x和y注册的平行四边形的面积
// 结果为(x[1] * y[2] - y[1] * x[2], x[2] * y[0] - y[2] * x[0], x[0] * y[1] - y[0] * x[1])
```
##### genType normalize(genType x)
``` glsl
// 归一化
```
##### genType faceforward(genType N, genType I, genType Nref)
``` glsl
// 如果 dot(Nref, I) < 0 返回 N，否则返回 -N
```
##### genType reflect(genType I, genType N)
``` glsl
// 返回光线反射向量
// 等价于 I - 2 * dot(N, I) * N
```
---
### 向量相关函数
##### bvec lessThan(vec x, vecy)
##### bvec lessThanEqual(vec x, vecy)
##### bvec greaterThan(vec x, vecy)
##### bvec greaterThanRqual(vec x, vecy)◊
##### bvec equal(vec x, vecy)
##### bvec notEqual(vec x, vecy)
##### bvec any(bvec x)
>如果向量x的任何组件为true，则结果返回true。
##### bvec all(bvec x)
>如果向量x的所有组件均为true，则结果返回true。
##### bvec not(bvec x)
>返回向量x的互补矩阵
---
### 材质查找函数
##### vec4 texture2D(sampler2D sampler, vec2 coord [, float bias])
##### vec4 texture2DProj(sampler2D sampler, vec3 coord [, float bias])
##### vec4 texture2DProj(sampler2D sampler, vec4 coord [, float bias])
##### vec4 texture2DLod(sampler2D sampler, vec2 coord, float lod)
##### vec4 texture2DProjLod(sampler2D sampler, vec3 coord, float lod)
##### vec4 texture2DProjLod(sampler2D sampler, vec4 coord, float lod)
##### vec4 textureCube(samplerCube sampler, vec3 coord [, float bias])
##### vec4 textureCubeLod(samplerCube sampler, vec3 coord, float lod)