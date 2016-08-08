
#GLSL �����ֲ�

###��������:

|����|˵��|
|---|---|
|__void__|������,���������κ�ֵ|
|__bool__|�������� true,false|
|__int__|�����ŵ����� signed integer|
|__float__|�����ŵĸ����� floating scalar|
|__vec2, vec3, vec4__|nά���������� n-component floating point vector|
|__bvec2, bvec3, bvec4__|nά�������� Boolean vector|
|__ivec2, ivec3, ivec4__|nά�������� signed integer vector|
|__mat2, mat3, mat4__|2x2, 3x3, 4x4 ���������� float matrix|
|__sampler2D__|2D���� a 2D texture|
|__samplerCube__|������ cube mapped texture|


###�����ṹ������:

|����|˵��|
|---|---|
|�ṹ|struct type-name{} ����c�����е� �ṹ��|
|����| float foo[3] glslֻ֧��1ά����,��������ǽṹ��ĳ�Ա|


###�����ķ�������:

glsl�е�����(vec2,vec3,vec4)����������ĺ���,������ܴ�����һ���ռ�����(x,y,z,w),���ߴ�����һ����ɫ(r,g,b,a),�ٻ��ߴ���һ����������(s,t,p,q) 
����glsl�ṩ��һЩ�����Ի��ķ������ʷ�ʽ.

`vector.xyzw`  ����xyzw �����������

`vector.rgba`  ����rgba �����������

`vector.stpq`  ����rgba �����������

```cpp
vec4 v=vec4(1.0,2.0,3.0,1.0);
float x = v.x; //1.0
float x1 = v.r; //1.0
float x2 = v[0]; //1.0

vec3 xyz = v.xyz; //vec3(1.0,2.0,3.0)
vec3 xyz1 = vec(v[0],v[1],v[2]); //vec3(1.0,2.0,3.0)
vec3 rgb = v.rgb; //vec3(1.0,2.0,3.0)

vec2 xyzw = v.xyzw; //vec4(1.0,2.0,3.0,1.0);
vec2 rgba = v.rgba; //vec4(1.0,2.0,3.0,1.0);

```

###�����:

|���ȼ�(ԽСԽ��)|�����|˵��|�����|
|---|---|---|---|
|1|__()__|����:a*(b+c)|N/A|
|2|__[] () . ++ --__ |�����±�__[]__,��������__fun(arg1,arg2,arg3)__,���Է���__a.b__,����/����׺__a++  a--__|L - R|
|3|__++ -- + - !__|����/��ǰ׺__++a  --a__,������(һ�����Ų�д)__a ,-a__,ȡ��__!false__|R - L|
|4|__* /__|�˳���ѧ����|L - R|
|5|__+ -__|�Ӽ���ѧ����|L - R|
|7|__< > <= >=__|��ϵ�����|L - R|
|8|__== !=__|����������|L - R|
|12|__&&__|�߼���|L - R|
|13|__^^__|�߼�������(�ô���������!=)|L - R|
|14|__\|\|__|�߼���|L - R|
|15|__? :__|��Ŀ�����|L - R|
|16|__= += -= *= /=__|��ֵ�븴�ϸ�ֵ|L - R|
|17|__,__|˳���������|L - R|

*ps ��ֵ����ֵ:*

    ��ֵ:��ʾһ������λ��,�����Ǳ���,Ҳ�����Ǳ��ʽ,�����ʽ���Ľ��������һ������λ��.

    ��ֵ:��ʾһ��ֵ, ������һ���������߱��ʽ�ٻ��ߴ����ֵ.

    �����������ȼ����������ж���������ı��ʽ����ֵ˳��ÿ�����������ȼ���ͬ.

    �������Ľ���ԣ�������ͬ���ȼ��Ĳ������Ǵ����Ҽ��㣬���Ǵ��ҵ�����㡣

###�������ͼ������:

glsl��,û����ʽ����ת��,ԭ����glslҪ���κα��ʽ��������(l-value),(r-value)�����ͱ���һ�� Ҳ����˵���±��ʽ���Ǵ����:

```cpp
int a =2.0; //����,r-valueΪfloat �� lvalue Ϊint.
int a =1.0+2;
float a =2;
float a =2.0+1;
bool a = 0; 
vec3 a = vec3(1.0, 2.0, 3.0) * 2;

```

__�������ֱ�˵˵�������������:__

__1.`float` �� `int`:__

 float��float , int��int֮���ǿ���ֱ�������,��float��int����.������Ҫ����һ����ʾת��.��Ҫô��floatת��int: __int(1.0)__ 
,Ҫô��intת��float: __float(1)__ ,���±��ʽ������ȷ��:

```javascript
int a=int(2.0);
float a= float(2);

int a=int(2.0)*2 + 1;
float a= float(2)*6.0+2.3;
```

__2.`float`  �� `vec(����)` `mat(����)`:__

vec,mat��Щ������ʵ����float���϶��ɵ�,��������float����ʱ,��ʵ������ÿһ�������Ϸֱ���float��������,�������ν��`�����`����.glsl��
�󲿷��漰vec,mat�����㶼��`�����`����,��Ҳ����ȫ��. �����оͻὲ������.

`�����`���������Ե�,�����˵ vec �� float ���������ǻ��� vec.

int �� vec,mat֮���ǲ��������, ��Ϊvec��mat�е�ÿһ���������� float ���͵�. �޷���int�������������.

����ö���˼��� float �� vec,mat ��������

```cpp
vec3 a = vec3(1.0, 2.0, 3.0);
mat3 m = mat3(1.0);
float s = 10.0;
vec3 b = s * a; // vec3(10.0, 20.0, 30.0)
vec3 c = a * s; // vec3(10.0, 20.0, 30.0)
mat3 m2 = s * m; // = mat3(10.0)
mat3 m3 = m * s; // = mat3(10.0)

```

__3. `vec(����)` �� `vec(����)`:__

�����������������Ҫ��֤�������Ľ�������ͬ.�����ܼ���.����: vec3*vec2 vec4+vec3 �ȵȶ��ǲ��е�.

���ǵļ��㷽ʽ������������ͬλ���ϵķ����ֱ��������,�䱾�ʻ�����������е�,���������˵��float���͵�
��������������һ������,��ͬ���� vec �� vec ���������� vec, �ҽ�������.

```cpp
vec3 a = vec3(1.0, 2.0, 3.0);
vec3 b = vec3(0.1, 0.2, 0.3);
vec3 c = a + b; // = vec3(1.1, 2.2, 3.3)
vec3 d = a * b; // = vec3(0.1, 0.4, 0.9)
```

![](img/webgl-glsl/2.png)

__3. `vec(����)` �� `mat(����)`:__

Ҫ��֤�������Ľ�����ͬ,��vec��mat��ֻ���ڳ˷�����.

���ǵļ��㷽ʽ�����Դ����еľ���˷���ͬ,�������������.


```cpp
vec2 v = vec2(10., 20.);
mat2 m = mat2(1., 2.,  3., 4.);
vec2 w = m * v; // = vec2(1. * 10. + 3. * 20., 2. * 10. + 4. * 20.)
...

vec2 v = vec2(10., 20.);
mat2 m = mat2(1., 2.,  3., 4.);
vec2 w = v * m; // = vec2(1. * 10. + 2. * 20., 3. * 10. + 4. * 20.)


```
���������ĳ˷���������:

![](img/webgl-glsl/3.png)


![](img/webgl-glsl/4.png)


__4. `mat(����)` �� `mat(����)`:__

Ҫ��֤�������Ľ�����ͬ.

��mat��mat��������, ���˳˷������Դ����еľ���˷���.�����������Ϊ���������.��˵����ֻ�г˷��������,���඼��vec��vec��������.

```cpp
mat2 a = mat2(1., 2.,  3., 4.);
mat2 b = mat2(10., 20.,  30., 40.);
mat2 c = a * b; //mat2(1.*10.+3.*20.,2.*10.+4.*20.,1.* 30.+3.*40.,2.* 30.+4.*40.);

mat2 d = a+b;//mat2(1.+10.,2.+20.,3.+30.,4.+40);

```
����˷���������:

![](img/webgl-glsl/5.png)


###�����޶���:

|���η�|˵��|
|---|---|
|__none__|(Ĭ�ϵĿ�ʡ��)���ر���,�ɶ���д,�������������������������|
|__const__|�������������Ĳ���Ϊֻ������|
|__attribute__|ֻ�ܴ�����vertex shader��,һ�����ڱ��涥���������,�����������ݻ������ж�ȡ����|
|__uniform__|������ʱshader�޷��ı�uniform����, һ���������ó��򴫵ݸ�shader�ı任���󣬲��ʣ����ղ����ȵ�.|
|__varying__|��Ҫ������vertex �� fragment ֮�䴫�ݱ��� |


__const__:

��C��������,��const�޶������εı�����ʼ���󲻿ɱ�,���˾ֲ�����,��������Ҳ����ʹ��const���η�.��Ҫע����ǽṹ����������const����,
���ṹ�е��ֶβ���.

const��������������ʱ�ͳ�ʼ�� `const vec3 v3 = vec3(0.,0.,0.)`

�ֲ�����ֻ��ʹ��const�޶���.

��������ֻ��ʹ��const�޶���.

```cpp
struct light {
        vec4 color;
        vec3 pos;
        //const vec3 pos1; //�ṹ�е��ֶβ�����const���λᱨ��.
    };
const light lgt = light(vec4(1.0), vec3(0.0)); //�ṹ����������const����

```

__attribute__:

attribute������`ȫ��`��`ֻ��`��,��ֻ����vertex shader��ʹ��,ֻ���븡����,���������������, 
һ��attribute�����������ó��򴫵�����ģ�Ͷ���,����,��ɫ,��������������Է������ݻ�����
(���ǵ�__gl.vertexAttribPointer__���������)

```cpp
attribute vec4 a_Position;

```

__uniform__:

uniform������`ȫ��`��`ֻ��`��,������shaderִ�����ǰ��ֵ����ı�,�����Ժ�����������ͱ������,
һ������ʹ��uniform�����������ⲿ���򴫵����Ļ�������(����Դλ��,ģ�͵ı任����ȵ�)
��Щ��������������Ȼ�ǲ���Ҫ���ı��.

```cpp
uniform vec4 lightPosition;

```

__varying__:

varying���ͱ����� vertex shader �� fragment shader ֮�����ʹ,һ�������� vertex shader ���޸���Ȼ����fragment shaderʹ����,��������
fragment shader���޸���.

```cpp
//������ɫ��
varying vec4 v_Color;
void main(){ 
    ...
    v_Color = vec4(1.,1.,1.,1);
}

//ƬԪ��ɫ��
...
varying vec4 v_Color;
void main() {
  gl_FragColor = v_Color;
}
...

```

Ҫע��ȫ�ֱ������Ʒ�ֻ��Ϊ const��attribute��uniform��varying�е�һ��.���ɸ���.

###���������޶���:

�����Ĳ���Ĭ�����Կ�������ʽ���ݵ�,Ҳ����ֵ����,�κδ��ݸ����������ı���,��ֵ���ᱻ����һ��,Ȼ���ٽ��������ڲ����д���.
���ǿ���Ϊ��������޶������ﵽ�������õ�Ŀ��,glsl���ṩ�Ĳ����޶�������:

|�޶���|˵��|
|---|---|
|< none: default >|Ĭ��ʹ�� in �޶���|
|in|���Ƶ��������ں����пɶ�д|
|out|����ʱ�Ӻ����и��Ƴ���|
|inout|���Ƶ������в��ڷ���ʱ���Ƴ���|


`in` �Ǻ���������Ĭ���޶���,�����������뺯���βε���ʵ��ʵ�ε�һ�ݿ���.�ں�����,�޸�in���ε��ββ���Ӱ�쵽ʵ�α�������.

`out` ���������������ⲿ������ֵ,outģʽ�´��ݽ����Ĳ�����write-only��(��д���ɶ�).������һ��"��λ",��λ�е�ֵ��Ҫ������������. 
�ں�����,�޸�out���ε��βλ�Ӱ�쵽ʵ�α���.

`inout` inout��,�βο��Ա����Ϊ��һ����ֵ��"��λ",���ɶ�Ҳ��д,�ں�����,�޸�inout���ε��βλ�Ӱ�쵽ʵ�α���.


###glsl�ĺ���:

glsl�����ڳ�������ⲿ��������.��������Ƕ��,���ܵݹ����,�ұ�����������ֵ����(�޷���ֵʱ����Ϊvoid) ����������glsl������c�����ǳ�����.

```cpp
vec4 getPosition(){ 
    vec4 v4 = vec4(0.,0.,0.,1.);
    return v4;
}

void doubleSize(inout float size){
    size= size*2.0  ;
}
void main() {
    float psize= 10.0;
    doubleSize(psize);
    gl_Position = getPosition();
    gl_PointSize = psize;
}

```




###���캯��:

glsl�б���������������ʱ���ʼ��,`float pSize = 10.0` Ҳ����������Ȼ�����Ҫ��ʱ���ڽ��и�ֵ.

�ۺ����Ͷ�����(����,����,����,�ṹ) ��Ҫʹ���乹�캯�������г�ʼ��. `vec4 color = vec4(0.0, 1.0, 0.0, 1.0);`

```cpp
//һ������
float pSize = 10.0;
float pSize1;
pSize1=10.0;
...

//��������
vec4 color = vec4(0.0, 1.0, 0.0, 1.0);
vec4 color1;
color1 =vec4(0.0, 1.0, 0.0, 1.0);
...

//�ṹ
struct light {
    float intensity;
    vec3 position;
};
light lightVar = light(3.0, vec3(1.0, 2.0, 3.0));

//����
const float c[3] = float[3](5.0, 7.2, 1.1);

```

###����ת��:

glsl����ʹ�ù��캯��������ʽ����ת��,��ֵ����:

```cpp
bool t= true;
bool f = false;

int a = int(t); //trueת��Ϊ1��1.0
int a1 = int(f);//falseת��Ϊ0��0.0

float b = float(t);
float b1 = float(f);

bool c = bool(0);//0��0.0ת��Ϊfalse
bool c1 = bool(1);//��0ת��Ϊtrue

bool d = bool(0.0);
bool d1 = bool(1.0);

```

###�����޶�:

glsl�ڽ��й�դ����ɫ��ʱ��,����������ĸ���������,��Щ��������ǵ�ǰ�豸�����ܳ��ܵ�,����glsl�ṩ��3�ָ���������,���ǿ��Ը��ݲ�ͬ���豸��ʹ�ú��ʵľ���.

�ڱ���ǰ����� `highp` `mediump` `lowp` ������ɶԸñ����ľ�������.

```
lowp float color;
varying mediump vec2 Coord;
lowp ivec2 foo(lowp mat3);
highp mat4 m;
```

����һ����ƬԪ��ɫ��(fragment shader)�ʼ�ĵط����� ` precision mediump float; ` ���趨��Ĭ�ϵľ���.��������û����ʽ�������ȵı���
���ᰴ���趨�õ�Ĭ�Ͼ���������.

__���ȷ������:__

�����ľ����������ɾ����޶���������,���û�о����޶���,��ҪѰ�����Ҳ���ʽ��,�Ѿ�ȷ�����ȵı���,һ���ҵ�,��ô�������ʽ�����ڸþ���������.����ҵ����,
��ѡ�񾫶Ƚϸߵ�����,���һ�����Ҳ���,��ʹ��Ĭ�ϻ����ľ�������.

```cpp
uniform highp float h1;
highp float h2 = 2.3 * 4.7; //������̺ͽ���� �Ǹ߾���
mediump float m;
m = 3.7 * h1 * h2; //������� �Ǹ߾���
h2 = m * h1; //������� �Ǹ߾���
m = h2 �C h1; //������� �Ǹ߾���
h2 = m + m; //������̺ͽ���� ���еȾ���
void f(highp float p); // �β� p �Ǹ߾���
f(3.3); //����� 3.3�Ǹ߾���


```


__invariant�ؼ���:__

����shader�ڱ���ʱ�����һЩ�ڲ��Ż�,���ܻᵼ��ͬ���������ڲ�ͬshader������һ����ȷ���.�������һЩ����,������vertx shader��fragmeng shader��ֵ��ʱ��.
����������Ҫʹ��`invariant` �ؼ�������ʽҪ����������뾫ȷһ��. ��Ȼ����Ҳ��ʹ�� `#pragma STDGL invariant(all)`��������������������뾫ȷһ��,
�����������Ʊ������Ż��̶�,��������.

```cpp
#pragma STDGL invariant(all) //�����������Ϊ invariant
invariant varying texCoord; //varying�ڴ������ݵ�ʱ������Ϊinvariant

```


__�޶�����˳��:__

����Ҫ�õ�����޶�����ʱ��Ҫ��ѭ����˳��:

1.��һ�������: invariant > storage > precision

2.�ڲ�����: storage > parameter > precision

����������˵��:

```cpp
invariant varying lowp float color; // invariant > storage > precision

void doubleSize(const in lowp float s){ //storage > parameter > precision
    float s1=s;
}

```




###Ԥ����ָ��:

�� # ��ͷ����Ԥ����ָ��,���õ���:
```cpp
#define #undef #if #ifdef #ifndef #else
#elif #endif #error #pragma #extension #version #line
```
���� __\#version 100__ ������˼�ǹ涨��ǰshaderʹ�� GLSL ES 1.00��׼���б���,���ʹ������Ԥ����ָ��,������������ڳ�����ʼλ��.

__���õĺ�:__

`__LINE__` : ��ǰԴ���е��к�. 

`__VERSION__` : һ������,ָʾ��ǰ��glsl�汾 ���� 100  ps: 100 = v1.00

`GL_ES` : �����ǰ���� OPGL ES ������������ GL_ES �����ó�1,һ��������鵱ǰ�����ǲ��� OPENGL ES.

`GL_FRAGMENT_PRECISION_HIGH` : �����ǰϵͳglsl��ƬԪ��ɫ��֧�ָ߸��㾫��,������Ϊ1.һ�����ڼ����ɫ������.

ʵ��:

1.���ͨ���ж�ϵͳ����,��ѡ����ʵľ���:
```cpp
#ifdef GL_ES //
#ifdef GL_FRAGMENT_PRECISION_HIGH
precision highp float;
#else
precision mediump float;
#endif
#endif

```

2.�Զ����:

```cpp
#define NUM 100
#if NUM==100
#endif
```

###���õ��������

glsl����ʹ��һЩ��������ñ�����Ӳ�����й�ͨ.���Ǵ��·ֳ����� һ���� `input`����,��������Ӳ��(��Ⱦ����)��������.
��һ����`output`����,���������ش�����,�Ա���ʱ��Ҫ.

__�� vertex Shader ��:__

output ���͵����ñ���:

|����|˵��|��λ|
|---|---|---|
|highp vec4 `gl_Position`;|gl\_Position ���ö���������Ϣ|vec4|
|mediump float `gl_PointSize`;|gl\_PointSize ��Ҫ���Ƶ�Ĵ�С,(ֻ��gl.POINTSģʽ����Ч) |float|


__�� fragment Shader ��:__

input ���͵����ñ���:

|����|˵��|��λ|
|---|---|---|
|mediump vec4 `gl_FragCoord`;|ƬԪ��framebuffer��������λ��|vec4|
|bool `gl_FrontFacing`;|��־��ǰͼԪ�ǲ�������ͼԪ��һ����|bool|
|mediump vec2 `gl_PointCoord`;|������ֵ��������������,��ķ�Χ��0.0��1.0|vec2|



output ���͵����ñ���:

|����|˵��|��λ|
|---|---|---|
|mediump vec4 `gl_FragColor`;|���õ�ǰƬ�����ɫ|vec4 RGBA color|
|mediump vec4 `gl_FragData[n]`|���õ�ǰƬ�����ɫ,ʹ��glDrawBuffers��������|vec4 RGBA color|


###���õĳ���

glsl�ṩ��һЩ���õĳ���,����˵����ǰϵͳ��һЩ����. ��ʱ������Ҫ�����Щ����,��shader��������Ż�,�ó�����ݶȸ���.

__�� vertex Shader ��:__

1.const mediump int `gl_MaxVertexAttribs`>=8

gl_MaxVertexAttribs ��ʾ��vertex shader(������ɫ��)�п��õ����attributes��.���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 8 ��.

2.const mediump int `gl_MaxVertexUniformVectors` >= 128

gl_MaxVertexUniformVectors ��ʾ��vertex shader(������ɫ��)�п��õ����uniform vectors��. ���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 128 ��.

3.const mediump int `gl_MaxVaryingVectors` >= 8

gl_MaxVaryingVectors ��ʾ��vertex shader(������ɫ��)�п��õ����varying vectors��. ���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 8 ��.

4.const mediump int `gl_MaxVertexTextureImageUnits` >= 0

gl_MaxVaryingVectors ��ʾ��vertex shader(������ɫ��)�п��õ��������Ԫ��(��ͼ). ���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
��������һ����û��(�޷���ȡ��������)

5.const mediump int `gl_MaxCombinedTextureImageUnits` >= 8

gl_MaxVaryingVectors ��ʾ�� vertex Shader��fragment Shader�ܹ����֧�ֶ��ٸ�����Ԫ. ���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 8 ��.


__�� fragment Shader ��:__

1.const mediump int `gl_MaxTextureImageUnits` >= 8

gl_MaxVaryingVectors ��ʾ�� fragment Shader(ƬԪ��ɫ��)���ܷ��ʵ��������Ԫ��,���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 8 ��.

2.const mediump int `gl_MaxFragmentUniformVectors` >= 16

gl_MaxFragmentUniformVectors ��ʾ�� fragment Shader(ƬԪ��ɫ��)�п��õ����uniform vectors��,���ֵ�Ĵ�Сȡ���� OpenGL ES ��ĳ�豸�ϵľ���ʵ��,
������Ͳ���С�� 16 ��.

3.const mediump int `gl_MaxDrawBuffers` = 1

gl_MaxDrawBuffers ��ʾ���õ�drawBuffers��,��OpenGL ES 2.0�����ֵΪ1, �ڽ����İ汾���ܻ������仯.



glsl�л���һ�����õ�uniform״̬����, `gl_DepthRange` ����������ȫ����ȷ�Χ.

�ṹ����:
```cpp
struct gl_DepthRangeParameters {
 highp float near; // n
 highp float far; // f
 highp float diff; // f - n
 };
 uniform gl_DepthRangeParameters gl_DepthRange;

```

���� gl\_DepthRange �������uniform״̬����������glsl 1.30 ��`����`.

###������

glsl�������ƺ�c���Էǳ�����,���ﲻ����������˵��,Ψһ��ͬ����Ƭ����ɫ������һ������Ŀ�����`discard`.
ʹ��discard���˳�Ƭ����ɫ������ִ�к����Ƭ����ɫ������Ƭ��Ҳ����д��֡��������

```cpp
for (l = 0; l < numLights; l++)
{
    if (!lightExists[l]);
        continue;
    color += light[l];
}
...

while (i < num)
{
    sum += color[i];
    i++;
}
...

do{
    color += light[lightNum];
    lightNum--;
}while (lightNum > 0)


...

if (true)
    discard;


```
 

###���ú�����

glsl�ṩ�˷ǳ��ḻ�ĺ�����,������ʹ��,��Щ���ܶ��Ƿǳ������һᾭ���õ���. ��Щ�������������ִ�Ŀ��Էֳ�7��:


__ͨ�ú���:__

�����е� ���� T������ float, vec2, vec3, vec4,�ҿ������������.

|����|˵��|
|---|---|
|T abs(T x)|����x�ľ���ֵ|
|T sign(T x)|�Ƚ�x��0��ֵ,����,����,С�� �ֱ𷵻� 1.0 ,0.0,-1.0|
|T floor(T x)|����<=x���������|
|T ceil(T x) |����>=����x����С����|
|T fract(T x)|��ȡx��С������|
|T mod(T x, T y) <br/> T mod(T x, float y) |ȡx,y������|
|T min(T x, T y) <br/> T min(T x, float y)|ȡx,y����Сֵ|
|T max(T x, T y) <br/> T max(T x, float y)|ȡx,y�����ֵ|
|T clamp(T x, T minVal, T maxVal) <br/>T clamp(T x, float minVal,float maxVal)|min(max(x, minVal), maxVal),����ֵ���޶��� minVal,maxVal֮��|
|T mix(T x, T y, T a) <br/>  T mix(T x, T y, float a)|ȡx,y�����Ի��,x*(1-a)+y\*a|
|T step(T edge, T x)  <br/> T step(float edge, T x)|��� x<edge ���� 0.0 ���򷵻�1.0|
|T smoothstep(T edge0, T edge1, T x) <br/> T smoothstep(float edge0,float edge1, T x) |���x<edge0 ���� 0.0 ���x>edge1����1.0, ���򷵻�Hermite��ֵ|



__�Ƕ�&���Ǻ���:__

�����е� ���� T������ float, vec2, vec3, vec4,�ҿ������������.

|����|˵��|
|---|---|
|T radians(T degrees) |�Ƕ�ת����|
|T degrees(T radians)|����ת�Ƕ�|
|T sin(T angle) |���Һ���,�Ƕ��ǻ���|
|T cos(T angle) |���Һ���,�Ƕ��ǻ���|
|T tan(T angle) |���к���,�Ƕ��ǻ���|
|T asin(T x) |�����Һ���,����ֵ�ǻ���|
|T acos(T x) |�����Һ���,����ֵ�ǻ���|
|T atan(T y, T x)<br/>  T atan(T y_over_x) |�����к���,����ֵ�ǻ���|
 



__ָ������:__

�����е� ���� T������ float, vec2, vec3, vec4,�ҿ������������.

|����|˵��|
|---|---|
|T pow(T x, T y)|����x��y���� x<sub>y</sub>|
|T exp(T x)|����x����Ȼָ���� e<sub>x</sub>|
|T log(T x)|����x����Ȼ���� ln|
|T exp2(T x)|����2��x���� 2<sub>x</sub>|
|T log2(T x)|����2Ϊ�׵Ķ��� log2|
|T sqrt(T x)|������ ��x|
|T inversesqrt(T x)|�ȿ�����,��ȡ����,���� 1/��x|



__���κ���:__

�����е� ���� T������ float, vec2, vec3, vec4,�ҿ������������.

|����|˵��|
|---|---|
|float length(T x)|����ʸ��x�ĳ���|
|float distance(T p0, T p1)|����p0  p1����ľ���|
|float dot(T x, T y)|����x y�ĵ��|
|vec3 cross(vec3 x, vec3 y)|����x y�Ĳ��|
|T normalize(T x)|��x���й�һ��,�����������򲻱䵫���ȱ�Ϊ1|
|T faceforward(T N, T I, T Nref)|���� ʸ�� N ��Nref ����������|
|T reflect(T I, T N)|���� I - 2 * dot(N,I) * N, ���������ʸ�� I ���ڷ�����N�� ���淴��ʸ��|
|T refract(T I, T N, float eta)|��������ʸ��I���ڷ�����N������ʸ��,������Ϊeta|



__������:__

mat����Ϊ�������;���.  

|����|˵��|
|---|---|
|mat matrixCompMult(mat x, mat y)|������ x �� y��Ԫ����������|


__��������:__

�����е� ���� T������ vec2, vec3, vec4, �ҿ������������.

bvecָ������bool������ɵ�һ������:

```cpp
vec3 v3= vec3(0.,0.,0.);
vec3 v3_1= vec3(1.,1.,1.);
bvec3 aa= lessThan(v3,v3_1); //bvec3(true,true,true)

```

|����|˵��|
|---|---|
|bvec lessThan(T x, T y) |������Ƚ�x < y,�����д��bvec��Ӧλ��|
|bvec lessThanEqual(T x, T y) |������Ƚ� x <= y,�����д��bvec��Ӧλ��|
|bvec  greaterThan(T x, T y) |������Ƚ� x > y,�����д��bvec��Ӧλ��|
|bvec greaterThanEqual(T x, T y) |������Ƚ�  x >= y,�����д��bvec��Ӧλ��|
|bvec equal(T x, T y) <br/> bvec equal(bvec x, bvec y)|������Ƚ� x == y,�����д��bvec��Ӧλ��|
|bvec notEqual(T x, T y) <br/> bvec notEqual(bvec x, bvec y)|������Ƚ� x!= y,�����д��bvec��Ӧλ��|
|bool any(bvec x)|���x������һ��������true,����Ϊtrue|
|bool all(bvec x)|���x�����з�����true,����Ϊtrue|
|bvec not(bvec x) |boolʸ���������ȡ��|



__�����ѯ����:__

ͼ������������ һ����ƽ��2d����,��һ���Ǻ�����,��Բ�ͬ�����������в�ͬ���ʷ���.

�����ѯ������Ŀ���Ǵ�sampler����ȡָ���������ɫ��Ϣ. �����д���Cube��������ָ ��Ҫ�����״����. ����Proj��������ָ��ͶӰ�İ汾. 

���º���ֻ��vertex shader�п���:
```cpp
vec4 texture2DLod(sampler2D sampler, vec2 coord, float lod);
vec4 texture2DProjLod(sampler2D sampler, vec3 coord, float lod);
vec4 texture2DProjLod(sampler2D sampler, vec4 coord, float lod);
vec4 textureCubeLod(samplerCube sampler, vec3 coord, float lod);

```


���º���ֻ��fragment shader�п���:

```cpp
vec4 texture2D(sampler2D sampler, vec2 coord, float bias);
vec4 texture2DProj(sampler2D sampler, vec3 coord, float bias);
vec4 texture2DProj(sampler2D sampler, vec4 coord, float bias);
vec4 textureCube(samplerCube sampler, vec3 coord, float bias);
```

�� vertex shader �� fragment shader �ж�����:

```cpp
vec4 texture2D(sampler2D sampler, vec2 coord);
vec4 texture2DProj(sampler2D sampler, vec3 coord);
vec4 texture2DProj(sampler2D sampler, vec4 coord);
vec4 textureCube(samplerCube sampler, vec3 coord);
```


###�ٷ���shader����:

�����shader��������һ�ۿ���,˵�����Ѿ���glsl���Ի���������.


__Vertex Shader:__

```cpp
uniform mat4 mvp_matrix; //͸�Ӿ��� * ��ͼ���� * ģ�ͱ任����
uniform mat3 normal_matrix; //���߱任����(��������任���߸��ű任)
uniform vec3 ec_light_dir; //���շ���
attribute vec4 a_vertex; // ��������
attribute vec3 a_normal; //���㷨��
attribute vec2 a_texcoord; //��������
varying float v_diffuse; //�����������ļн�
varying vec2 v_texcoord; //2d��������
void main(void)
{
 //��һ������
 vec3 ec_normal = normalize(normal_matrix * a_normal);
 //v_diffuse �Ƿ�������յļн�.����������˷���,������������Ϊ1�� �˻���cos��ֵ
 v_diffuse = max(dot(ec_light_dir, ec_normal), 0.0);
 v_texcoord = a_texcoord;
 gl_Position = mvp_matrix * a_vertex;
}
```

__Fragment Shader:__

```cpp
precision mediump float;
uniform sampler2D t_reflectance;
uniform vec4 i_ambient;
varying float v_diffuse;
varying vec2 v_texcoord;
void main (void)
{
 vec4 color = texture2D(t_reflectance, v_texcoord);
 //����ֽ⿪���� color*vec3(1,1,1)*v_diffuse + color*i_ambient
 //ɫ*��*�н�cos + ɫ*������
 gl_FragColor = color*(vec4(v_diffuse) + i_ambient);
}
```