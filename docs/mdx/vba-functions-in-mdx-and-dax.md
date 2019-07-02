---
title: Funciones de VBA en MDX y DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4f6b6d89ced88a570ce242ae9490d4c6d8bd6ac8
ms.sourcegitcommit: 0b0f5aba602732834c8439c192d95921149ab4c3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2019
ms.locfileid: "67500048"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funciones de VBA en MDX y DAX


  Este documento contiene una referencia cruzada de todas las funciones VBA disponibles en [Visual Basic para aplicaciones de funciones](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) que se admiten en MDX; Además, la lista incluye una nota cuando hay una equivalencia funcional con el lenguaje DAX .  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Referencia de funciones de Visual Basic para Aplicaciones  
  
|Nombre de la función|Admitida|Notas|  
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
|date|Solo MDX|**Advertencia** DAX implementa otra función con el mismo nombre; la función DATE (Year, Month, Day), utilizada para generar un valor de tipo de fecha de los argumentos proporcionados|  
|DateAdd|Solo MDX|**Advertencia** DAX implementa otra función con el mismo nombre; el DATEADD (\<fechas >, < number_of_intervals >,\<intervalo >) función, utilizada para desplazar las fechas proporcionadas por un número de intervalos especificado|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
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
|Filter|No compatible|**Advertencia** MDX implementa otra función con el mismo nombre; la función de filtro (expresión_conjunto, Filter) devuelve el conjunto resultante de filtrar un conjunto especificado según una condición de búsqueda de los argumentos proporcionados<br /><br /> **Advertencia** DAX implementa otra función con el mismo nombre; el filtro (\<tabla >,\<filtro >) función devuelve una tabla que representa un subconjunto de otra tabla o expresión de los argumentos proporcionados|  
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
|Iif|Solo MDX|**Advertencia** DAX implementa una función similar con el nombre: IF (logical_test, value_if_true, value_if_false) función.|  
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
|NPer|Solo MDX||  
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
|String|Solo MDX||  
|StrReverse|No compatible||  
|Modificador|Solo MDX||  
|SYD|Solo MDX||  
|Pestaña|No compatible||  
|Tan|Solo MDX||  
|Time|No compatible||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|No compatible||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|No compatible||  
|Weekday|DAX, MDX||  
|WeekdayName|No compatible||  
|Year|DAX, MDX||  
  
  
