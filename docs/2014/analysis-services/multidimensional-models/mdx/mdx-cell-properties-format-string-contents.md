---
title: FORMAT_STRING, contenido (MDX) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- formats [Analysis Services], string values
- VALUE property
- formats [Analysis Services], numeric values
- FORMATTED_VALUE property
- FORMAT_STRING contents
ms.assetid: c354c938-0328-4b8e-adc5-3b52fd2a7152
caps.latest.revision: 28
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 198fadc6d3f2e1599c98ba5146e830fef5b8be17
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37293595"
---
# <a name="formatstring-contents-mdx"></a>FORMAT_STRING, contenido (MDX)
  El `FORMAT_STRING` formatos de la propiedad de celda el `VALUE` propiedad de celda, crea el valor para el `FORMATTED_VALUE` propiedad de celda. El `FORMAT_STRING` propiedad de celda controla los valores sin procesar numéricos y de cadena, aplicando una expresión de formato con respecto al valor para devolver un valor con formato para el `FORMATTED_VALUE` propiedad de celda. En las siguientes tablas se detallan la sintaxis y los caracteres de formato utilizados para controlar los valores numéricos y de cadena.  
  
## <a name="string-values"></a>Valores de cadena  
 Una expresión de formato para cadenas puede tener una sección o dos, separadas con punto y coma (;).  
  
|Uso|Resultado|  
|-----------|------------|  
|Una sección|El formato se aplica a todos los valores de cadena.|  
|Dos secciones|La primera sección se aplica a los datos de cadena, mientras que la segunda sección se aplica a los valores NULL y a las cadenas de longitud cero ("").|  
  
 Los caracteres descritos en la siguiente tabla pueden aparecer en la cadena de formato para las cadenas de caracteres.  
  
|Carácter|Descripción|  
|---------------|-----------------|  
|@|Representa un marcador de posición de caracteres que muestra un carácter o espacio. Si la cadena tiene un carácter en la posición donde aparece el signo @ en la cadena de formato, se muestra el carácter en la cadena con formato. De lo contrario, en esa posición de la cadena con formato se muestra un espacio. Los marcadores de posición se rellenan de derecha a izquierda, a menos que haya un signo de exclamación (!) en la cadena de formato.|  
|&|Representa un marcador de posición de caracteres que muestra un carácter o nada. Si la cadena tiene un carácter en la posición donde aparece el signo "y" comercial (&), se muestra el carácter en la cadena con formato. De lo contrario, no se muestra nada en la cadena con formato. Los marcadores de posición se rellenan de derecha a izquierda, a menos que haya un signo de exclamación (!) en la cadena de formato.|  
|\<|Fuerza el uso de minúsculas. La cadena con formato muestra todos los caracteres en minúscula.|  
|>|Fuerza el uso de mayúsculas. La cadena con formato muestra todos los caracteres en mayúscula.|  
|!|Fuerza que se rellenen de izquierda a derecha los marcadores de posición. (El valor predeterminado es rellenar los marcadores de posición de derecha a izquierda).|  
  
## <a name="numeric-values"></a>Valores numéricos  
 Una expresión de formato definida por el usuario para números puede tener de una a cuatro secciones separadas con punto y coma. Si el argumento de formato contiene uno de los formatos numéricos con nombre, únicamente se permite una sección.  
  
|Uso|Resultado|  
|-----------|------------|  
|Una sección|La expresión de formato se aplica a todos los valores.|  
|Dos secciones|La primera sección se aplica a valores positivos y ceros; la segunda se aplica a valores negativos.|  
|Tres secciones|La primera sección se aplica a valores positivos, la segunda a valores negativos y la tercera a los ceros.|  
|Cuatro secciones|La primera sección se aplica a valores positivos, la segunda a valores negativos, la tercera a los ceros y la cuarta a valores NULL.|  
  
 El siguiente ejemplo tiene dos secciones. La primera sección define el formato de los valores positivos y los ceros, y la segunda define el formato de los valores negativos.  
  
```  
"$#,##0;($#,##0)"  
```  
  
 Si incluye signos de punto y coma sin nada entre ellos, la sección que falta se imprime utilizando el formato de los valores positivos. Por ejemplo, el siguiente formato muestra los valores positivos y negativos utilizando el formato de la primera sección y muestra "Zero" si el valor es cero:  
  
```  
"$#,##0;;\Z\e\r\o"  
```  
  
 En la siguiente tabla se identifican los caracteres que pueden aparecer en la cadena de formato para formatos numéricos.  
  
|Carácter|Descripción|  
|---------------|-----------------|  
|None|Muestra el número sin formato.|  
|**0**|Representa un marcador de posición de dígitos que muestra un dígito o un cero (0).<br /><br /> Si el número tiene un dígito en la posición donde aparece el cero en la cadena de formato, se muestra el dígito en el valor con formato. De lo contrario, el valor con formato muestra un cero en dicha posición.<br /><br /> Si el número tiene menos dígitos que ceros (en cualquier lado del separador decimal) en la cadena de formato, el valor con formato muestra ceros a la izquierda o a la derecha.<br /><br /> Si el número tiene más dígitos a la derecha del separador decimal que ceros a la derecha del separador decimal en la expresión de formato, el valor con formato redondea el número con tantos decimales como ceros haya.<br /><br /> Si el número tiene más dígitos a la izquierda del separador decimal que ceros a la izquierda del separador decimal en la expresión de formato, el valor con formato muestra los dígitos adicionales sin modificación.|  
|**#**|Representa un marcador de posición de dígitos que muestra un dígito o nada.<br /><br /> Si la expresión tiene un dígito en la posición donde aparece el signo de número (**#**) en la cadena de formato, el valor con formato muestra el dígito. De lo contrario, el valor con formato no muestra nada en dicha posición.<br /><br /> El marcador de posición de signo de número (**#**) funciona como el marcador de posición de dígito cero (**0**), excepto que no se muestran ceros a la izquierda ni a la derecha si el número tiene los mismos dígitos o menos que el número de caracteres **#** a cualquier lado del separador decimal en la expresión de formato.|  
|**.**|Representa un marcador de posición de decimales que determina cuántos dígitos se muestran a la izquierda o a la derecha del separador decimal.<br /><br /> Si la expresión de formato solo contiene caracteres de signos de número (**#**) a la izquierda del separador (**,**), los números inferiores a 1 empiezan con un separador decimal. Para mostrar un cero a la izquierda con los números fraccionarios, utilice un cero (0) como primer marcador de posición de dígitos a la izquierda del separador decimal.<br /><br /> El carácter real utilizado como marcador de posición de decimales en la salida con formato depende del formato de número que reconozca el sistema informático.<br /><br /> Nota: En algunas configuraciones regionales se utiliza la coma como separador decimal.|  
|**%**|Representa un marcador de posición de porcentaje. La expresión se multiplica por 100. El carácter de porcentaje (**%**) se inserta en la posición donde aparece el porcentaje en la cadena de formato.|  
|**,**|Representa un separador de miles que separa los millares de las centenas en un número que tiene cuatro o más posiciones a la izquierda del separador decimal.<br /><br /> El uso estándar del separador de miles se especifica si el formato contiene un separador de miles delimitado por marcadores de posición de dígitos (**0** o **#**).<br /><br /> Dos separadores de miles adyacentes o un separador de miles inmediatamente a la izquierda del separador decimal (tanto si se ha especificado un decimal como si no), significan "escalar el número dividiéndolo por 1000, redondeándolo como sea preciso". Por ejemplo, puede usar la cadena de formato "**##0**,," para representar 100 millones como 100. Los números menores que 1 millón se muestran como 0. Dos separadores de miles adyacentes en cualquier posición que no sea la inmediatamente a la izquierda del separador decimal se tratan como si especificaran el uso de un separador de miles.<br /><br /> El carácter real utilizado como separador de miles en la salida con formato depende del formato de número que reconozca el sistema informático.<br /><br /> Nota: En algunas configuraciones regionales se utiliza el punto como separador de miles.|  
|**:**|Representa un separador de hora que separa horas, minutos y segundos cuando se asigna formato a los valores de hora.<br /><br /> Nota: En algunas configuraciones regionales se utilizan otros caracteres como separador de hora.<br /><br /> El carácter real utilizado como separador de hora en la salida con formato viene determinado por la configuración del sistema del equipo.|  
|**/**|Representa un separador de fecha que separa el día, el mes y el año cuando se asigna formato a los valores de fecha.<br /><br /> El carácter real utilizado como separador de fecha en la salida con formato viene determinado por la configuración del sistema del equipo.<br /><br /> Nota: En algunas configuraciones regionales se utilizan otros caracteres como separador de fecha.|  
|**E- E+ e- e+**|Representa el formato científico.<br /><br /> Si la expresión de formato contiene como mínimo un marcador de posición de dígito (**0** o **#**) a la derecha de **E-**, **E+**, **e-** o **e+**, el valor con formato se muestra en formato científico y se inserta E o e entre el número y su exponente. El número de marcadores de posición de dígitos a la derecha determina el número de dígitos del exponente. Use **E-** o **e-** para incluir un signo menos junto a los exponentes negativos. Use **E+** o **e+** para incluir un signo menos junto a los exponentes negativos y un signo más junto a los exponentes positivos.|  
|**- + $ ( )**|Muestra un carácter literal.<br /><br /> Para mostrar un carácter distinto del que aparece en la lista, escriba una barra diagonal inversa (**\\**) antes del carácter o delimite el carácter con comillas dobles (**" "**).|  
|**\\**|Muestra el siguiente carácter en la cadena de formato.<br /><br /> Para mostrar un carácter con un significado especial como un carácter literal, escriba una barra diagonal inversa (**\\**) antes del carácter. La barra diagonal inversa no se muestra. Utilizar una barra diagonal inversa es equivalente a delimitar el siguiente carácter con comillas dobles. Para mostrar una barra diagonal inversa, use dos barras diagonales inversas (**\\\\**). A continuación se indican algunos ejemplos de caracteres que no pueden mostrarse como caracteres literales:<br /><br /> Los caracteres de formato de fecha y hora:**a**, **c**, **d**, **h**, **m**, **n**, **p**, **q**, **s**, **t**, **w**, **y**, **/** y **:**<br /><br /> Los caracteres de formato numérico:**#**, **0**, **%**, **E**, **e**, **coma**y **punto**<br /><br /> Los caracteres de formato de cadena:**@**, **&**, **\<**, **>** y **!**|  
|**"ABC"**|Muestra la cadena entre comillas dobles (**" "**).<br /><br /> Para asignar formato a una cadena desde dentro del código, use Chr(**34**) para delimitar el texto. (El código de carácter para las comillas dobles es **34**).|  
  
### <a name="named-numeric-formats"></a>Formatos numéricos con nombre  
 La tabla siguiente muestra los nombres de formato numérico predefinidos:  
  
|Nombre de formato|Descripción|  
|-----------------|-----------------|  
|`General Number`|Muestra el número sin separadores de miles.|  
|`Currency`|Muestra el número con separador de miles, si es apropiado. Muestra dos dígitos a la derecha del separador decimal. El resultado dependerá de la configuración regional.|  
|`Fixed`|Muestra al menos un dígito a la izquierda y dos a la derecha del separador de decimales.|  
|`Standard`|Muestra el número con separador de miles, al menos un dígito a la izquierda y dos a la derecha del separador de decimales.|  
|`Percent`|Muestra el número multiplicado por 100 con un signo de porcentaje (%) anexado a la derecha. Siempre muestra dos dígitos a la derecha del separador decimal.|  
|`Scientific`|Utiliza la notación científica estándar.|  
|`Yes/No`|Muestra No si el número es 0; de lo contrario, muestra Yes.|  
|`True/False`|Muestra False si el número es 0; de lo contrario, muestra True.|  
|`On/Off`|Muestra Off si el número es 0; de lo contrario, muestra On.|  
  
## <a name="date-values"></a>Valores de fecha  
 En la siguiente tabla se identifican los caracteres que pueden aparecer en la cadena de formato para formatos de fecha y hora.  
  
|Carácter|Descripción|  
|---------------|-----------------|  
|**:**|Representa un separador de hora que separa horas, minutos y segundos cuando se asigna formato a los valores de hora.<br /><br /> El carácter real utilizado como separador de hora en la salida con formato viene determinado por la configuración del sistema del equipo.<br /><br /> Nota: En algunas configuraciones regionales se utilizan otros caracteres como separador de hora.|  
|**/**|Representa un separador de fecha que separa el día, el mes y el año cuando se asigna formato a los valores de fecha.<br /><br /> El carácter real utilizado como separador de fecha en la salida con formato viene determinado por la configuración del sistema del equipo.<br /><br /> Nota: En algunas configuraciones regionales se utiliza otro carácter como separador de fecha.|  
|**C**|Muestra la fecha como **ddddd** y la hora como **ttttt**, en este orden.<br /><br /> Muestra únicamente información de fecha si no hay ninguna parte fraccionaria en el número de serie de fecha. Muestra únicamente información de hora si no hay ninguna parte entera.|  
|**d**|Muestra el día como un número sin un cero a la izquierda (1–31).|  
|**dd**|Muestra el día como un número con un cero a la izquierda (01–31).|  
|**ddd**|Muestra el día como una abreviatura (Dom–Sáb).|  
|**dddd**|Muestra el día con el nombre completo (Domingo-Sábado).|  
|**ddddd**|Muestra la fecha como una fecha completa (día, mes y año), con el formato que especifique la configuración de formato de fecha corto del sistema.<br /><br /> En Microsoft Windows, el formato de fecha corta predeterminado es **d/m/aa**.|  
|**dddddd**|Muestra un número de serie de fecha como fecha completa (día, mes y año), con el formato de fecha largo que especifique la configuración del sistema.<br /><br /> En Windows, el formato largo de fecha predeterminado es **dd de mmmm de yyyy**.|  
|**w**|Muestra el día de la semana como un número (del 1 para el domingo al 7 para el sábado).|  
|**ww**|Muestra la semana del año como un número (1–54).|  
|**m**|Muestra el mes como un número sin un cero a la izquierda (1–12).<br /><br /> Si **m** va inmediatamente después de **h** o **hh**, se muestra el minuto en lugar del mes.|  
|**mm**|Muestra el mes como un número con un cero a la izquierda (01–12).<br /><br /> Si **m** va inmediatamente después de **h** o **hh**, se muestra el minuto en lugar del mes.|  
|**mmm**|Muestra el mes como una abreviatura (Ene–Dic).|  
|**mmmm**|Muestra el mes con el nombre completo (Enero–Diciembre).|  
|**q**|Muestra el trimestre del año como un número (1–4).|  
|**y**|Muestra el día del año como un número (1–366).|  
|**yy**|Muestra el año como un número de dos dígitos (00–99).|  
|**aaaa**|Muestra el año como un número de cuatro dígitos (100–9999).|  
|**h**|Muestra la hora como un número sin ceros a la izquierda (0–23).|  
|**hh**|Muestra la hora como un número con ceros a la izquierda (00–23).|  
|**n**|Muestra el minuto como un número sin ceros a la izquierda (0–59).|  
|**nn**|Muestra el minuto como un número con ceros a la izquierda (00–59).|  
|**s**|Muestra el segundo como un número sin ceros a la izquierda (0–59).|  
|**ss**|Muestra el segundo como un número con ceros a la izquierda (00–59).|  
|**t t t t t**|Muestra la hora como una hora completa (hora, minuto y segundo), utilizando el separador de hora definido en el formato de hora que reconozca el equipo.<br /><br /> Si se selecciona la opción de cero a la izquierda, se muestra un cero a la izquierda, y la hora es anterior a 10:00 tanto en ciclo a.m. como p.m. Por ejemplo, 09:59,<br /><br /> En Windows, el formato de hora predeterminado es **h:mm:ss**.|  
|**AM/PM**|Muestra **AM** en mayúscula con las horas desde medianoche hasta mediodía; muestra **PM** en mayúscula con las horas desde mediodía hasta medianoche.<br /><br /> Nota: Utiliza el reloj de 12 horas.|  
|**am/pm**|Muestra **am** en minúscula con las horas desde medianoche hasta mediodía; muestra **pm** en minúscula con las horas desde mediodía hasta medianoche.<br /><br /> Nota: Utiliza el reloj de 12 horas.|  
|**A/P**|Muestra una **A** en mayúscula con las horas desde medianoche hasta mediodía; muestra una **P** en mayúscula con las horas desde mediodía hasta medianoche.<br /><br /> Nota: Utiliza el reloj de 12 horas.|  
|**a/p**|Muestra **a** en minúscula con las horas desde medianoche hasta mediodía; muestra **p** en minúscula con las horas desde mediodía hasta medianoche.<br /><br /> Nota: Utiliza el reloj de 12 horas.|  
|**AMPM**|Muestra el literal de cadena AM como está definido en el equipo con las horas desde medianoche hasta mediodía; muestra el literal de cadena PM como está definido en el equipo con las horas desde mediodía hasta medianoche.<br /><br /> Nota: Utiliza el reloj de 12 horas.<br /><br /> **AMPM** puede ir en mayúscula o en minúscula, pero la cadena que se muestra aparecerá como esté definida en la configuración del equipo.<br /><br /> En Windows, el formato predeterminado es **a. m./p. m.**|  
  
### <a name="named-date-formats"></a>Formatos de fecha con nombre  
 La tabla siguiente identifica los nombres de formatos de fecha y hora predefinidos:  
  
|Nombre de formato|Descripción|  
|-----------------|-----------------|  
|`General Date`|Muestra una fecha o una hora. Para los números reales, muestra una fecha y hora, por ejemplo, 4/3/93 05:34 PM. Si no hay ninguna parte fraccionaria, muestra solo una fecha, por ejemplo, 4/3/93. Si no hay ninguna parte entera, solo muestra un tiempo, por ejemplo, 05:34 PM. La configuración del sistema determina el formato de la presentación de la fecha.|  
|`Long Date`|Muestra una fecha según el formato de fecha larga del sistema.|  
|`Medium Date`|Muestra una fecha utilizando el formato de fecha medio adecuado para el idioma de la aplicación host.|  
|`Short Date`|Muestra una fecha con el formato de fecha corta del sistema.|  
|`Long Time`|Muestra una hora de acuerdo con el formato de hora larga vigente en la referencia cultural actual; incluye normalmente horas, minutos y segundos.|  
|`Medium Time`|Muestra una hora en el formato de 12 horas utilizando horas y minutos y el designador de AM/PM.|  
|`Short Time`|Muestra una hora utilizando el formato de 24 horas, por ejemplo, 17:45.|  
  
## <a name="see-also"></a>Vea también  
 [LANGUAGE y FORMAT_STRING en FORMATED_VALUE](mdx-cell-properties-formatted-value-property.md)   
 [Uso de las propiedades de celda &#40;MDX&#41;](mdx-cell-properties-using-cell-properties.md)   
 [Creación y uso de los valores de propiedad &#40;MDX&#41;](../../creating-and-using-property-values-mdx.md)   
 [Aspectos básicos de consultas MDX &#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
