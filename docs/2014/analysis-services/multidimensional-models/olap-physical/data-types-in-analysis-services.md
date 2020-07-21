---
title: Tipos de datos en Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
ms.assetid: 910be4f4-3010-41cd-9fdc-f0a79a0ce823
author: minewiskan
ms.author: owend
ms.openlocfilehash: 06b93090918a0fffc9c98e1560b338177eff3d84
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545933"
---
# <a name="data-types-in-analysis-services"></a>Tipos de datos en Analysis Services
  Para todos los <xref:Microsoft.AnalysisServices.DataItem> objetos, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite el siguiente subconjunto de `System.Data.OleDb.OleDbType` . Para establecer o leer el tipo de datos, utilice el [tipo de datos dataitem &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl).  
  
## <a name="supported-data-types"></a>Tipos de datos admitidos  
  
|||  
|-|-|  
|BigInt|Entero de 64 bits con signo. El tipo de valor *BigInt* representa los enteros con valores comprendidos entre los valores de 9223372036854775808 negativos y los 9.223.372.036.854.775.807 positivos.|  
|Binary|Flujo de datos binarios de tipo **byte** . **Byte** es un tipo de valor que representa enteros sin signo con valores comprendidos entre 0 y 255.|  
|Boolean|Las instancias de este tipo tienen el valor `true` o `false`.|  
|Moneda|Un valor de *moneda* comprendido entre-922.337.203.685.477,5808 y + 922.337.203.685.477,5807 con una precisión de una diezmilésima de unidad de moneda (cuatro posiciones decimales).|  
|Fecha|Datos de fecha y hora, almacenados como valor double. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción de un día o de una hora del día.|  
|Double|Número de coma flotante de comprendido entre -1,79769313486232E +308 y 1,79769313486232E +308. Un valor Double almacena información numérica con una precisión de hasta 15 dígitos decimales.|  
|Entero|Entero de 32 bits que representa números enteros con signo con valores que comprendes desde el número 2.147.483.648 negativo hasta el número 2.147.483.647 positivo.|  
|Single|Número de coma flotante comprendido entre - 3,4028235E +38 y 3,4028235E +38. Un valor Single almacena información numérica con una precisión de hasta siete dígitos decimales.|  
|Smallint|Entero de 16 bits con signo. El tipo de valor *smallint* representa enteros con signo con valores comprendidos entre el 32768 negativo y el 32767 positivo.|  
|Tinyint|Entero de 8 bits con signo. El tipo de valor Tinyint representa los enteros con valores que comprenden desde el número 128 negativo al número 127 positivo.|  
|UnsignedBigInt|Entero de 64 bits sin signo. El tipo de valor *UnsignedBigInt* representa enteros sin signo con valores comprendidos entre 0 y 18446744073709551615.|  
|UnsignedInt|Entero de 32 bits sin signo. El tipo de valor *UnsignedInt* representa enteros sin signo con valores comprendidos entre 0 y 4.294.967.295.|  
|UnsignedSmallInt|Entero de 16 bits sin signo. El tipo de valor *UnsignedSmallInt* representa enteros sin signo con valores comprendidos entre 0 y 65535.|  
|UnsignedTinyInt|Entero de 8 bits sin signo. El tipo de valor *UnsignedTinyInt* representa enteros sin signo con valores comprendidos entre 0 y 255|  
|WChar|Flujo de caracteres Unicode terminado en NULL. *WCHAR* es una colección secuencial de caracteres Unicode que se utiliza para representar texto.|  
  
## <a name="amo-validations-on-data-types"></a>Validaciones de AMO en tipos de datos  
 En la siguiente tabla se enumeran las validaciones adicionales que Objetos de administración de análisis (AMO) hace para determinados enlaces:  
  
|Object|Enlace|Tipos de datos admitidos|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Todos excepto Binary|  
||NameColumn|Solo WChar|  
||SkippedLevelsColumn|Solo tipos integer: BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|Solo WChar|  
||CustomRollupPropertiesColumn|Solo WChar|  
||UnaryOperatorColumn|Solo WChar|  
||ValueColumn|Todo|  
|AttributeTranslation|CaptionColumn|Solo WChar|  
|ScalarMiningStructureColumn|KeyColumns|Todos excepto Binary|  
||NameColumn|Solo WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|Todos excepto Binary|  
|MeasureGroupAttribute|KeyColumns|Todos excepto Binary|  
|Medida de recuento distintiva|Source|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
