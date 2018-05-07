---
title: Las funciones de VBA en MDX y DAX | Documentos de Microsoft
ms.custom: ''
ms.date: 01/30/2018
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 420452fd-9507-4093-8857-71d3e70d96cc
caps.latest.revision: 11
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 6dce57c7a8043a8d25b31b389e47763df261baa8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funciones de VBA en MDX y DAX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Este documento contiene una referencia cruzada de todas las funciones VBA disponibles en [de Visual Basic para aplicaciones de funciones](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) que se admiten en MDX; Además, la lista incluye una nota cuando hay una equivalencia funcional con el lenguaje DAX .  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Referencia de funciones de Visual Basic para Aplicaciones  
  
|Nombre de la función|Compatible|Notas|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Array|No compatible||  
|Asc|Solo MDX||  
|AscW|Solo MDX||  
|Atn|Solo MDX||  
|CallByName|No compatible||  
|CBool|Solo MDX||  
|CByte|Solo MDX||  
|CCur|Solo MDX||  
|CDate|Solo MDX||  
|CDbl|Solo MDX||  
|CDec|Solo MDX||  
|Choose|Solo MDX||  
|Chr|Solo MDX||  
|CInt|Solo MDX||  
|CLng|Solo MDX||  
|CLngLng|No compatible||  
|CLngPtr|No compatible||  
|Comando|No compatible||  
|Cos|Solo MDX||  
|CreateObject|No compatible||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|No compatible||  
|CVar|Solo MDX||  
|CVErr|No compatible||  
|Date|Solo MDX|**Advertencia** DAX implementa otra función con el mismo nombre; la función de fecha (año, mes, día), utilizada para generar un valor de tipo de fecha de los argumentos proporcionados|  
|DateAdd|Solo MDX|**Advertencia** DAX implementa otra función con el mismo nombre; el DATEADD (\<fechas >, < number_of_intervals >\<intervalo >) función, que se usa para desplazar las fechas proporcionadas por un número de intervalos especificado|  
|DateDiff]|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue]|DAX, MDX||  
|Day|DAX, MDX||  
|DDB|Solo MDX||  
|Dir|No compatible||  
|DoEvents|No compatible||  
|Environ|No compatible||  
|EOF|No compatible||  
|Error|No compatible||  
|Exp|DAX, MDX||  
|FileAttr|No compatible||  
|FileDateTime|No compatible||  
|FileLen|No compatible||  
|Filtro|No compatible|**Advertencia** MDX implementa otra función con el mismo nombre; la función FILTER (función, Filter) devuelve el conjunto resultante de filtrar un conjunto especificado en función de una condición de búsqueda de los argumentos proporcionados<br /><br /> **Advertencia** DAX implementa otra función con el mismo nombre; el filtro (\<tabla >,\<filtro >) función devuelve una tabla que representa un subconjunto de otra tabla o expresión de los argumentos proporcionados|  
|Fix|Solo MDX||  
|Format (Visual Basic para Aplicaciones)|DAX, MDX||  
|FormatCurrency|No compatible||  
|FormatDateTime|No compatible||  
|FormatNumber|No compatible||  
|FormatPercent|No compatible||  
|FreeFile|No compatible||  
|FV|Solo MDX||  
|GetAllSettings|No compatible||  
|GetAttr|No compatible||  
|GetObject|No compatible||  
|GetSetting|No compatible||  
|Hex|Solo MDX||  
|Hour|DAX, MDX||  
|Iif|Solo MDX|**Advertencia** DAX implementa una función similar con el nombre: IF (logical_test, value_if_true, value_if_false) (función).|  
|IMEStatus|No compatible||  
|Entrada|No compatible||  
|InputBox|No compatible||  
|InStr|Solo MDX||  
|InStrRev|No compatible||  
|int|DAX, MDX||  
|IPmt|Solo MDX||  
|IRR|Solo MDX||  
|IsArray|Solo MDX||  
|Sólo IsDateMDX||  
|IsEmpty|Solo MDX||  
|IsError|DAX, MDX||  
|IsMissing|Solo MDX||  
|IsNull|Solo MDX||  
|IsNumeric|Solo MDX||  
|IsObject|No compatible||  
|Join|No compatible||  
|LBound|No compatible||  
|LCase|Solo MDX||  
|Izquierda|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|No compatible||  
|LOF|No compatible||  
|Log|Solo MDX|**Importante** DAX implementa otra función con el mismo nombre; la función LOG (number, base). Devuelve el logaritmo de un número en la base de los argumentos proporcionados.|  
|LTrim|Solo MDX||  
|MacID|No compatible||  
|MacScript|No compatible||  
|Mid|DAX, MDX||  
|Minute|DAX, MDX||  
|MIRR|Solo MDX||  
|Month|DAX, MDX||  
|MonthName|No compatible||  
|MsgBox|No compatible||  
|Ahora|DAX, MDX||  
|NPer]|Solo MDX||  
|NPV|Solo MDX||  
|Oct|Solo MDX||  
|Partición|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|Rate|Solo MDX||  
|Reemplazar|No compatible||  
|RGB|Solo MDX||  
|Derecha|DAX, MDX||  
|Rnd|Solo MDX||  
|Redondear|DAX, MDX||  
|RTrim|Solo MDX||  
|Second|DAX, MDX||  
|Seek|No compatible||  
|Sgn|DAX, MDX||  
|Shell|No compatible||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Space|Solo MDX||  
|Spc|No compatible||  
|división|No compatible||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|Cadena]|Solo MDX||  
|StrReverse|No compatible||  
|Switch|Solo MDX||  
|SYD|Solo MDX||  
|Pestaña|No compatible||  
|Tan|Solo MDX||  
|Time|No compatible||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Recorte]|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|No compatible||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|No compatible||  
|Weekday|DAX, MDX||  
|WeekdayName|No compatible||  
|Year|DAX, MDX||  
  
  
