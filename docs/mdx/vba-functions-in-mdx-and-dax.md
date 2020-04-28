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
ms.openlocfilehash: 39a0db181f3b1d1a40af1a5fa27ba78366a9d2b3
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68135018"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funciones de VBA en MDX y DAX


  Este documento contiene una referencia cruzada de todas las funciones de VBA disponibles en [Visual Basic para aplicaciones funciones](https://msdn.microsoft.com/vba/language-reference-vba/articles/functions-visual-basic-for-applications) que se admiten en MDX; Además, la lista incluye una nota cuando hay una equivalencia funcional con el lenguaje DAX.  
  
## <a name="visual-basic-for-applications-functions-reference"></a>Referencia de funciones de Visual Basic para Aplicaciones  
  
|Nombre de la función|Compatible|Notas|  
|-------------------|---------------|-----------|  
|Abs|DAX, MDX||  
|Matriz|Incompatible||  
|Asc|Solo MDX||  
|AscW|Solo MDX||  
|Atn|Solo MDX||  
|CallByName|Incompatible||  
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
|CLngLng|Incompatible||  
|CLngPtr|Incompatible||  
|Get-Help|Incompatible||  
|Cos|Solo MDX||  
|CreateObject|Incompatible||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|Incompatible||  
|CVar|Solo MDX||  
|CVErr|Incompatible||  
|Date|Solo MDX|**ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función DATE (Year, month, Day), que se usa para generar un valor de tipo Date a partir de los argumentos especificados.|  
|DateAdd|Solo MDX|**ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función DATEADD\<(dates>, <number_of_intervals\<>, Interval>), que se usa para desplazar las fechas dadas por un número de intervalos determinados|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
|Día|DAX, MDX||  
|DDB|Solo MDX||  
|Dir|Incompatible||  
|DoEvents|Incompatible||  
|Environ|Incompatible||  
|EOF|Incompatible||  
|Error|Incompatible||  
|Exp|DAX, MDX||  
|FileAttr|Incompatible||  
|FileDateTime|Incompatible||  
|FileLen|Incompatible||  
|Filter|Incompatible|**ADVERTENCIA** de MDX implementa una función diferente con el mismo nombre. la función FILTER (Set_Expression, Logical_Expression) devuelve el conjunto resultante de filtrar un conjunto especificado en función de una condición de búsqueda de los argumentos especificados.<br /><br /> **ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función FILTER\<(tabla>\<, Filter>) devuelve una tabla que representa un subconjunto de otra tabla o expresión de los argumentos especificados|  
|Fix|Solo MDX||  
|Format (Visual Basic para Aplicaciones)|DAX, MDX||  
|FormatCurrency|Incompatible||  
|FormatDateTime|Incompatible||  
|FormatNumber|Incompatible||  
|FormatPercent|Incompatible||  
|FreeFile|Incompatible||  
|FV|Solo MDX||  
|GetAllSettings|Incompatible||  
|GetAttr|Incompatible||  
|GetObject|Incompatible||  
|GetSetting|Incompatible||  
|Hex|Solo MDX||  
|Hour|DAX, MDX||  
|Iif|Solo MDX|**ADVERTENCIA** de DAX implementa una función similar con la función Name: IF (logical_test, value_if_true, value_if_false).|  
|IMEStatus|Incompatible||  
|Entrada|Incompatible||  
|InputBox|Incompatible||  
|InStr|Solo MDX||  
|InStrRev|Incompatible||  
|Int|DAX, MDX||  
|IPmt|Solo MDX||  
|IRR|Solo MDX||  
|IsArray|Solo MDX||  
|Solo IsDateMDX||  
|IsEmpty|Solo MDX||  
|IsError|DAX, MDX||  
|IsMissing|Solo MDX||  
|IsNull|Solo MDX||  
|IsNumeric|Solo MDX||  
|IsObject|Incompatible||  
|Join|Incompatible||  
|LBound|Incompatible||  
|LCase|Solo MDX||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|Incompatible||  
|LOF|Incompatible||  
|Log|Solo MDX|**Importante** DAX implementa una función diferente con el mismo nombre. la función LOG (número, base). Devuelve el logaritmo de un número en la base de los argumentos proporcionados.|  
|LTrim|Solo MDX||  
|MacID|Incompatible||  
|MacScript|Incompatible||  
|Mid|DAX, MDX||  
|Minute|DAX, MDX||  
|MIRR|Solo MDX||  
|Mes|DAX, MDX||  
|MonthName|Incompatible||  
|MsgBox|Incompatible||  
|Ahora|DAX, MDX||  
|NPer|Solo MDX||  
|NPV|Solo MDX||  
|Oct|Solo MDX||  
|Partition|Solo MDX||  
|Pmt|Solo MDX||  
|PPmt|Solo MDX||  
|PV|Solo MDX||  
|QBColor|Solo MDX||  
|Tarifa|Solo MDX||  
|Replace|Incompatible||  
|RGB|Solo MDX||  
|Right|DAX, MDX||  
|Rnd|Solo MDX||  
|Round|DAX, MDX||  
|RTrim|Solo MDX||  
|Segundo|DAX, MDX||  
|Seek|Incompatible||  
|Sgn|DAX, MDX||  
|Shell|Incompatible||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Space|Solo MDX||  
|Spc|Incompatible||  
|Dividir|Incompatible||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|String|Solo MDX||  
|StrReverse|Incompatible||  
|Modificador|Solo MDX||  
|SYD|Solo MDX||  
|Pestaña|Incompatible||  
|Tan|Solo MDX||  
|Tiempo|Incompatible||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Trim|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|Incompatible||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|Incompatible||  
|Día de la semana|DAX, MDX||  
|WeekdayName|Incompatible||  
|Año|DAX, MDX||  
  
  
