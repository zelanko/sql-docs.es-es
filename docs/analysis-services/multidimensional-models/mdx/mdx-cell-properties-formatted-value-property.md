---
title: LANGUAGE y FORMAT_STRING en FORMATTED_VALUE | Documentos de Microsoft
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7534ff5f-954e-47d4-a2ed-4b5b8ccb30e6
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0e69f9e798dd5922bae7c677fc599c8f82293ee1
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-cell-properties---formattedvalue-property"></a>Propiedades de celda MDX - FORMATTED_VALUE, propiedad
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]La propiedad FORMATTED_VALUE se basa en las interacciones de las propiedades VALUE, FORMAT_STRING y LANGUAGE de la celda. En este tema se explica cómo interactúan estas propiedades para generar la propiedad FORMATTED_VALUE.  
  
## <a name="value-formatstring-language-properties"></a>Propiedades VALUE, FORMAT_STRING y LANGUAGE  
 En la tabla siguiente se explica en qué consisten estas propiedades para ayudar a preparar su uso de forma conjunta.  
  
 VALUE  
 Valor sin formato de la celda.  
  
 FORMAT_STRING  
 Plantilla de formato que se va a aplicar al valor de la celda para generar la propiedad FORMATTED_VALUE.  
  
 LANGUAGE  
 Especificación de la configuración regional que se va a aplicar junto a FORMAT_STRING para generar una versión localizada de FORMATTED_VALUE.  
  
## <a name="formattedvalue-constructed"></a>Composición de la propiedad FORMATTED_VALUE  
 La propiedad FORMATTED_VALUE se construye utilizando el valor de la propiedad VALUE y aplicando a dicho valor la plantilla de formato especificada en la propiedad FORMAT_STRING. Además, cuando el valor de formato es un **literal de formato con nombre** , la especificación de la propiedad LANGUAGE modifica la salida de FORMAT_STRING para adaptarse al uso del lenguaje del formato con nombre. Todos los literales del formato con nombre están definidos de forma que se pueden localizar. Por ejemplo, `"General Date"` es una especificación que puede adaptarse, a diferencia de la plantilla `"YYYY-MM-DD hh:nn:ss",` , que establece que la fecha debe presentarse tal y como se define en la plantilla con independencia de la especificación del idioma.  
  
 Si surge algún conflicto entre la plantilla FORMAT_STRING y la especificación de LANGUAGE, la plantilla FORMAT_STRING invalida la especificación de LANGUAGE. Por ejemplo, si FORMAT_STRING="$ #0", LANGUAGE=1034 (España) y VALUE=123.456, el valor de FORMATTED_VALUE será "$ 123" en lugar de "€ 123", pues dado que el valor de la plantilla de formato invalida el idioma especificado, el formato esperado será en euros.  
  
### <a name="examples"></a>Ejemplos  
 En los ejemplos siguientes se muestra la salida que se obtiene cuando LANGUAGE se utiliza junto con FORMAT_STRING.  
  
 En el primer ejemplo se explica el formato de los valores numéricos; en el segundo ejemplo se explica el formato de los valores de fecha y hora.  
  
 En todos los ejemplos se utiliza el código MDX (Expresiones multidimensionales).  
  
 `with`  
  
 `member measures.A as 5040, FORMAT_STRING="Currency"`  
  
 `member measures.B as measures.A, LANGUAGE=1034`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="$#,##0.00"`  
  
 `member measures.D as measures.A, FORMAT_STRING="Scientific"`  
  
 `member measures.E as measures.A, LANGUAGE=1034 , FORMAT_STRING="Scientific"`  
  
 `member measures.F as 0.5040, FORMAT_STRING="Percent"`  
  
 `member measures.G as measures.F, LANGUAGE=1034`  
  
 `member measures.H as 0, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.I as 59, LANGUAGE=1034 , FORMAT_STRING="Yes/No"`  
  
 `member measures.J as 0, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `member measures.K as -312, LANGUAGE=1034 , FORMAT_STRING="ON/OFF"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F, measures.G, measures.H, measures.I, measures.J, measures.K} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Cuando la consulta MDX anterior se ejecuta utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] sobre un servidor y un cliente con la configuración regional 1033, los resultados (transpuestos) son los siguientes:  
  
|Miembro|FORMATTED_VALUE|Explicación|  
|------------|----------------------|-----------------|  
|Un|$5,040.00|FORMAT_STRING se establece en `Currency` y LANGUAGE es `1033`al heredar el valor de la configuración regional del sistema.|  
|B|€5.040,00|FORMAT_STRING se establece en `Currency` (al heredar de A) y LANGUAGE se establece explícitamente en `1034` (España); por tanto, se usa el signo de euro, además de un separador decimal y un separador de miles diferentes.|  
|C|$5.040,00|FORMAT_STRING se establece en `$#,##0.00` e invalida a Currency (heredado de A) y LANGUAGE se establece explícitamente en `1034` (España). Dado que la propiedad FORMAT_STRING establece de forma explícita el símbolo de moneda en $, FORMATTED_VALUE se presenta con el signo $. Sin embargo, dado que `.` (punto) y `,` (coma) son respectivamente los marcadores de posición del separador decimal y el separador de miles, la especificación del lenguaje tiene efecto a la hora de generar una salida adaptada para el separador decimal y el separador de miles.|  
|D|5.04E+03|FORMAT_STRING se establece en `Scientific` y LANGUAGE en `1033`, al heredar el valor de la configuración regional del sistema; por tanto, `.` (punto) será el separador decimal.|  
|E|5,04E+03|FORMAT_STRING se establece en `Scientific` y LANGUAGE se establece explícitamente en `1034,` , por tanto, `,` (coma) será el separador decimal.|  
|F|50,40 %|FORMAT_STRING se establece en `Percent` y LANGUAGE en `1033`, al heredar el valor de la configuración regional del sistema; por tanto, `.` (punto) será el separador decimal.<br /><br /> Observe que VALUE se ha modificado de 5040 a 0.5040|  
|G|50,40 %|FORMAT_STRING se establece en `Percent`, al heredar de F, y LANGUAGE se establece explícitamente en `1034` ; por tanto, `,` (coma) será el separador decimal.<br /><br /> Observe que VALUE se ha heredado del valor F.|  
|H|no|FORMAT_STRING se establece en `YES/NO`, VALUE se establece en 0 y LANGUAGE se establece explícitamente en `1034`; como no hay diferencia entre el inglés NO y el español NO, el usuario no puede apreciar ninguna diferencia en FORMATTED_VALUE.|  
|I|SI|FORMAT_STRING se establece en `YES/NO`, VALUE se establece en 59 y LANGUAGE se establece explícitamente en `1034`; tal y como se definió para el formato YES/NO, cualquier valor que no sea cero (0) es YES y, dado que el idioma está establecido en español, FORMATTED_VALUE es SI.|  
|J|Desactivado|FORMAT_STRING se establece en `ON/OFF`, VALUE se establece en 0 y LANGUAGE se establece explícitamente en `1034`; tal y como se definió para el formato ON/OFF, cualquier valor igual a cero (0) es OFF y, dado que el idioma se estableció en español, FORMATTED_VALUE es Desactivado.|  
|K|Activado|FORMAT_STRING se establece en `ON/OFF`, VALUE se establece en -312 y LANGUAGE se establece explícitamente en `1034`; tal y como se definió en el formato de ON/OFF, cualquier valor distinto de (0) es ON, y dado que el idioma está establecido en español, el valor de FORMATTED_VALUE es Activado.|  
  
 `with`  
  
 `member measures.A as 'CDate("1959-03-12 06:30")'`  
  
 `member measures.B as measures.A, FORMAT_STRING="Long Date"`  
  
 `member measures.C as measures.A, LANGUAGE=1034 , FORMAT_STRING="General Date"`  
  
 `member measures.D as measures.A, LANGUAGE=1034, FORMAT_STRING="Long Date"`  
  
 `member measures.E as measures.A, LANGUAGE=1041 , FORMAT_STRING="General Date"`  
  
 `member measures.F as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Date"`  
  
 `member measures.G as measures.A, FORMAT_STRING="Long Time"`  
  
 `member measures.H as measures.A, FORMAT_STRING="Short Time"`  
  
 `member measures.I as measures.A, LANGUAGE=1034 , FORMAT_STRING="Long Time"`  
  
 `member measures.J as measures.A, LANGUAGE=1034 , FORMAT_STRING="Short Time"`  
  
 `member measures.K as measures.A, LANGUAGE=1041 , FORMAT_STRING="Long Time"`  
  
 `member measures.L as measures.A, LANGUAGE=1041 , FORMAT_STRING="Short Time"`  
  
 `Select {measures.A, measures.B, measures.C, measures.D, measures.E, measures.F`  
  
 `, measures.G, measures.H, measures.I, measures.J, measures.K, measures.L} on 0`  
  
 `from [Adventure Works]`  
  
 `cell properties VALUE, FORMAT_STRING, LANGUAGE, FORMATTED_VALUE`  
  
 Cuando la consulta MDX anterior se ejecuta utilizando [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] sobre un servidor y un cliente con la configuración regional 1033, los resultados (transpuestos) son los siguientes:  
  
|Miembro|FORMATTED_VALUE|Explicación|  
|------------|----------------------|-----------------|  
|Un|3/12/1959 6:30:00 AM|FORMAT_STRING se establece implícitamente en `General Date` a través de la expresión CDate() y LANGUAGE es `1033` (inglés), al heredar el valor de la configuración regional del sistema.|  
|B|Thursday, March 12, 1959|FORMAT_STRING se establece explícitamente en `Long Date` y LANGUAGE es `1033` (inglés) al heredar el valor de la configuración regional del sistema.|  
|C|12/03/1959 6:30:00|FORMAT_STRING se establece explícitamente en `General Date` y LANGUAGE en `1034` (español).<br /><br /> Observe que el mes y el día cambian de lugar con respecto al estilo de formato de EE.UU.|  
|D|jueves, 12 de marzo de 1959|FORMAT_STRING se establece explícitamente en `Long Date` y LANGUAGE en `1034` (español).<br /><br /> Observe que el mes y el día de la semana se expresan alfabéticamente en español.|  
|E|1959/03/12 6:30:00|FORMAT_STRING se establece explícitamente en `General Date` y LANGUAGE en `1041` (japonés).<br /><br /> Observe que la fecha tiene ahora el formato Año/Mes/Día Hora:Minutos:Segundos.|  
|F|1959年3月12日|FORMAT_STRING se establece explícitamente en `Long Date` y LANGUAGE en `1041` (japonés).|  
|G|6:30:00 a.m.|FORMAT_STRING se establece explícitamente en `Long Time` y LANGUAGE es `1033` (inglés), al heredar el valor de la configuración regional del sistema.|  
|H|06:30|FORMAT_STRING se establece explícitamente en `Short Time` y LANGUAGE es `1033` (inglés), al heredar el valor de la configuración regional del sistema.|  
|I|6:30:00|FORMAT_STRING se establece explícitamente en `Long Time` y LANGUAGE en `1034` (español).|  
|J|06:30|FORMAT_STRING se establece explícitamente en `Short Time` y LANGUAGE en `1034` (español).|  
|K|6:30:00|FORMAT_STRING se establece explícitamente en `Long Time` y LANGUAGE en `1041` (japonés).|  
|L|06:30|FORMAT_STRING se establece explícitamente en `Short Time` y LANGUAGE en `1041` (japonés).|  
  
## <a name="see-also"></a>Vea también  
 [FORMAT_STRING, contenido &#40;MDX&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-format-string-contents.md)   
 [Mediante las propiedades de celda &#40; MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-cell-properties-using-cell-properties.md)   
 [Creación y uso de valores de propiedad &#40; MDX &#41;](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)   
 [Aspectos básicos de las consultas MDX &#40;Analysis Services&#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
