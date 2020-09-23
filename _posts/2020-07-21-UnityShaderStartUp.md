---
layout: post
title:  "My Simple Fire Effect"
date:   2020-07-21 21:59:10 +0900
categories: UnityShaderStartUp
---
I have started to learn Unity Shader StartUp for technical artist.

Today, I learned how to make fire effect with simple UV manipulation.
Thus, I would post it how to do.

WARNING! : This is simple and easy way to make. I and study material does not care any sort of optimizations.

First of all, this book introduce three condition to look like fire.

```
What do we consider to make fire

1. It does not affected by light sources.
2. It is transparent.
3. It moves.
```

First condition, lights.

When you made simple texture only surface shader. You might use o.Albedo.
However, o.Albedo takes light calculation. It does light calculation.
Thus, in order to avoid light calculation, we have to use o.Emission to choose final pixel color.

```
// surf function
void surf (Input IN, inout SurfaceOutputStandard o)
{
    fixed4 c = tex2D (_MainTex, IN.uv_MainTex);
    o.Emission = c.rgb * d.rgb;
    o.Alpha = c.a * d.a;
}
```

Second condition, transparent.

Originally, I thought we can use alpha value with o.Alpha but the Alpha of surface shader is not working what I thought. In order to use the Alpha variable, we have to handle more fundamental parts of Unity Shader and know much more concepts. (Alpha is handled differently than normal objects, and also one of the most heavy calculation.)
Therefore, we need another solution.
Luckily, the book told me two parts which changed.
```
1. Change RenderType

Tags { "RenderType" = "Opaque"}

->

Tags { "RenderType" = "Transparent" "Queue" = "Transparent" }
```
```
2. Change #pragma line


#pragma surface surf Standard ...

->

#pragma surface surf Standard alpha:fade
```
I don't know why that changes make object transparent but let the book tell me later.

Third condition, move like a fire.

The book introduces two ways.
Both of them use two textures.

1. Multiply of two Images.
2. Use Noise Image as secondary Texture.

First Solution, 1. Multiply of two Images.
Based on first image which look like idle fire itself.
![fireTest.tga](/assets/MySimpleFireEffect/fireTest.tga)

Add secondary image which look smoke of fire.

![4_2.tga](/assets/MySimpleFireEffect/4_2.tga)

After put them together in same shader. Make second image moves to upward and multiply them rgb, and alpha value seperately.

```
        void surf (Input IN, inout SurfaceOutputStandard o)
        {
            fixed4 c = tex2D (_MainTex, IN.uv_MainTex);
            fixed4 d = tex2D(_SecondaryTex, fixed2(IN.uv_SecondaryTex.x, IN.uv_SecondaryTex.y - (_Time.y * _Scaler)));

            o.Emission = c.rgb * d.rgb;
            o.Alpha = c.a * d.a;
        }
```

Then result is going to be like this.

[Result of Simple Image]

Second Solution, 2. Use Noise Image as secondary Texture.
Same as previous case, use same Image as Primary Image.

However, we are going to use Noise texture as secondary texture.
Noise texture look like this

![noise2.png](/assets/MySimpleFireEffect/noise2.png)

We move noise texture based on time and plus or minus any component of Noise's color.
Then this calculation makes fire shimmer.

Code would be this.
```
        void surf (Input IN, inout SurfaceOutputStandard o)
        {
            // Albedo comes from a texture tinted by color
            fixed4 d = tex2D(_SecondTex, IN.uv_SecondTex - _Time.y);
            fixed4 c = tex2D (_MainTex, IN.uv_MainTex - (d.r * _Scaler));
            o.Albedo = c.rgb;
            o.Alpha = c.a;
        }
```

As I mentioned before, this is simple and the most easy way to do this. They are not optimized and take a lot of resources. I made this to practice UV manipulation not a real world technical artist job. I hope you know I'm on learning stage.

Thank you for reading my fire effect posting and see you with different topics.
