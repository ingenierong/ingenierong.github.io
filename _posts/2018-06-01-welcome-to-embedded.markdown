---
layout: post
title:  "Bienvenido al mundo de los empotrados!!!"
date:   2018-06-01 15:40:56
categories: embedded development sofware
---

El mundo de los sistemas empotrados es maravillosamente vesatil, permite a los desarrolladores crear proyectos interesantes todos los dias. Se trata de un mundo muy ligado al Hardware, en ocasiones se programa directamente en C realizando accesos a los registros del procesador.

En muchas ocasiones, resulta dificil trabajar con este tipo de sistemas. Muchos de estos sistemas son lentos y disponen de escasos recursos para su depuracion (en ocasiones ninguno).

Asi suele verse el codigo C para un sistema empotrado:

{% highlight C %}

void SystemInit_ExtMemCtl(void)
{
    __IO uint32_t tmp = 0x00;

    register uint32_t tmpreg = 0, timeout = 0xFFFF;
    register __IO uint32_t index;
    RCC->AHB1ENR |= 0x000001F8;
    tmp = READ_BIT(RCC->AHB1ENR, RCC_AHB1ENR_GPIOCEN);
    GPIOD->AFR[0] = 0x00CCC0CC;
    GPIOD->AFR[1] = 0xCCCCCCCC;
    GPIOD->MODER = 0xAAAA0A8A;
    GPIOD->OSPEEDR = 0xFFFF0FCF;
    GPIOD->OTYPER = 0x00000000;
    GPIOD->PUPDR = 0x00000000;
    GPIOE->AFR[0] = 0xC00CC0CC;
    GPIOE->AFR[1] = 0xCCCCCCCC;
    GPIOE->MODER = 0xAAAA828A;
    GPIOE->OSPEEDR = 0xFFFFC3CF;
    GPIOE->OTYPER = 0x00000000;
    GPIOE->PUPDR = 0x00000000;
    // ...
    /* Delay */
    for (index = 0; index<1000; index++);
    // ...
    (void)(tmp);
}
{% endhighlight %}

Como podemos ver no es el codigo mas elegante del mundo.


[jekyll-gh]: https://github.com/mojombo/jekyll
[jekyll]:    http://jekyllrb.com
