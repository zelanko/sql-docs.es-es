---
description: Funciones de VBA en MDX y DAX
title: Funciones de VBA en MDX y DAX | Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0dcbf0f0321ddc0c1959c4681c0b1dddf49c1aba
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/19/2020
ms.locfileid: "92192295"
---
# <a name="vba-functions-in-mdx-and-dax"></a>Funciones de VBA en MDX y DAX


  Este documento contiene una referencia cruzada de todas las funciones de VBA disponibles en [Visual Basic para aplicaciones funciones](/office/vba/Language/Reference/functions-visual-basic-for-applications) que se admiten en MDX; Además, la lista incluye una nota cuando hay una equivalencia funcional con el lenguaje DAX.  
  
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
|Elegir|Solo MDX||  
|Chr|Solo MDX||  
|CInt|Solo MDX||  
|CLng|Solo MDX||  
|CLngLng|No compatible||  
|CLngPtr|No compatible||  
|Get-Help|No compatible||  
|Cos|Solo MDX||  
|CreateObject|No compatible||  
|CSng|Solo MDX||  
|CStr|Solo MDX||  
|CurDir|No compatible||  
|CVar|Solo MDX||  
|CVErr|No compatible||  
|Date|Solo MDX|**ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función DATE (Year, month, Day), que se usa para generar un valor de tipo Date a partir de los argumentos especificados.|  
|DateAdd|Solo MDX|**ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función DATEADD ( \<dates> , <number_of_intervals>, \<interval> ) que se usa para desplazar las fechas dadas por un número de intervalos determinados|  
|DateDiff|Solo MDX||  
|DatePart|Solo MDX||  
|DateSerial|Solo MDX||  
|DateValue|DAX, MDX||  
|Día|DAX, MDX||  
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
|Filter|No compatible|**ADVERTENCIA** de MDX implementa una función diferente con el mismo nombre. la función FILTER (Set_Expression, Logical_Expression) devuelve el conjunto resultante de filtrar un conjunto especificado en función de una condición de búsqueda de los argumentos especificados.<br /><br /> **ADVERTENCIA** de DAX implementa una función diferente con el mismo nombre. la función FILTER ( \<table> , \<filter> ) devuelve una tabla que representa un subconjunto de otra tabla o expresión de los argumentos especificados|  
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
|Hora|DAX, MDX||  
|Iif|Solo MDX|**ADVERTENCIA** de DAX implementa una función similar con la función Name: IF (logical_test, value_if_true, value_if_false).|  
|IMEStatus|No compatible||  
|Entrada|No compatible||  
|InputBox|No compatible||  
|InStr|Solo MDX||  
|InStrRev|No compatible||  
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
|IsObject|No compatible||  
|Join|No compatible||  
|LBound|No compatible||  
|LCase|Solo MDX||  
|Left|DAX, MDX||  
|Len|DAX, MDX||  
|Loc|No compatible||  
|LOF|No compatible||  
|Log|Solo MDX|**Importante** DAX implementa una función diferente con el mismo nombre. la función LOG (número, base). Devuelve el logaritmo de un número en la base de los argumentos proporcionados.|  
|LTrim|Solo MDX||  
|MacID|No compatible||  
|MacScript|No compatible||  
|Mid|DAX, MDX||  
|Minute|DAX, MDX||  
|MIRR|Solo MDX||  
|Mes|DAX, MDX||  
|MonthName|No compatible||  
|MsgBox|No compatible||  
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
|Replace|No compatible||  
|RGB|Solo MDX||  
|Right|DAX, MDX||  
|Rnd|Solo MDX||  
|Round|DAX, MDX||  
|RTrim|Solo MDX||  
|Second|DAX, MDX||  
|Seek|No compatible||  
|Sgn|DAX, MDX||  
|Shell|No compatible||  
|Sin|Solo MDX||  
|SLN|Solo MDX||  
|Space|Solo MDX||  
|Spc|No compatible||  
|Dividir|No compatible||  
|Sqr|Solo MDX||  
|Str|Solo MDX||  
|StrComp|Solo MDX||  
|StrConv|Solo MDX||  
|String|Solo MDX||  
|StrReverse|No compatible||  
|Conmutador|Solo MDX||  
|SYD|Solo MDX||  
|Pestaña|No compatible||  
|Tan|Solo MDX||  
|Time|No compatible||  
|Timer|Solo MDX||  
|TimeSerial|Solo MDX||  
|TimeValue|DAX, MDX||  
|Recortar|DAX, MDX||  
|TypeName|Solo MDX||  
|UBound|No compatible||  
|UCase|Solo MDX||  
|Val|Solo MDX||  
|VarType|No compatible||  
|Día de la semana|DAX, MDX||  
|WeekdayName|No compatible||  
|Year|DAX, MDX||  
  
