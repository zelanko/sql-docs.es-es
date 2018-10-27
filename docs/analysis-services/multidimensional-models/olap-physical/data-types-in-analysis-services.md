---
title: Tipos de datos en Analysis Services | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ea192588186f69adbc04ab6a56123206e1fb7817
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146460"
---
# <a name="data-types-in-analysis-services"></a>Tipos de datos en Analysis Services
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Para todos los <xref:Microsoft.AnalysisServices.DataItem> objetos, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] admite el subconjunto siguiente de **System.Data.OleDb.OleDbType**. Para establecer o leer el tipo de datos, utilice [tipo de datos DataItem &#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/data-type/dataitem-data-type-assl).  
  
## <a name="supported-data-types"></a>Tipos de datos admitidos  
  
|||  
|-|-|  
|Bigint|Entero de 64 bits con signo. El *BigInt* tipo de valor representa los enteros con valores comprendidos entre el número 9.223.372.036.854.775.808 negativo al número 9.223.372.036.854.775.807 positivo.|  
|Binario|Un flujo de datos binarios de **bytes** tipo. **Bytes** es un tipo de valor que representa los enteros sin signo con valores comprendidos entre 0 y 255.|  
|Boolean|Las instancias de este tipo tienen el valor **true** o **false**.|  
|Moneda|Un *moneda* valor comprendido entre -922.337.203.685.477,5808 y + 922.337.203.685.477,5807 con una precisión de una diezmilésima de unidad de moneda (cuatro lugares decimales).|  
|date|Datos de fecha y hora, almacenados como valor double. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción de un día o de una hora del día.|  
|Doble|Número de coma flotante de comprendido entre -1,79769313486232E +308 y 1,79769313486232E +308. Un valor Double almacena información numérica con una precisión de hasta 15 dígitos decimales.|  
|Integer|Entero de 32 bits que representa números enteros con signo con valores que comprendes desde el número 2.147.483.648 negativo hasta el número 2.147.483.647 positivo.|  
|Único|Número de coma flotante comprendido entre - 3,4028235E +38 y 3,4028235E +38. Un valor Single almacena información numérica con una precisión de hasta siete dígitos decimales.|  
|Smallint|Entero de 16 bits con signo. El *Smallint* tipo de valor representa los enteros con signo con valores comprendidos entre 32768 negativo al número 32767 positivo.|  
|Tinyint|Entero de 8 bits con signo. El tipo de valor Tinyint representa los enteros con valores que comprenden desde el número 128 negativo al número 127 positivo.|  
|UnsignedBigInt|Entero de 64 bits sin signo. El *UnsignedBigInt* tipo de valor representa los enteros sin signo con valores comprendidos entre 0 y 18.446.744.073.709.551.615.|  
|UnsignedInt|Entero de 32 bits sin signo. El *UnsignedInt* tipo de valor representa los enteros sin signo con valores comprendidos entre 0 y 4.294.967.295.|  
|UnsignedSmallInt|Entero de 16 bits sin signo. El *UnsignedSmallInt* tipo de valor representa los enteros sin signo con valores comprendidos entre 0 y 65535.|  
|UnsignedTinyInt|Entero de 8 bits sin signo. El *UnsignedTinyInt* tipo de valor representa los enteros sin signo con valores comprendidos entre 0 y 255.|  
|WChar|Flujo de caracteres Unicode terminado en NULL. Un *WChar* es una colección secuencial de caracteres Unicode que se utiliza para representar texto.|  
  
## <a name="amo-validations-on-data-types"></a>Validaciones de AMO en tipos de datos  
 En la siguiente tabla se enumeran las validaciones adicionales que Objetos de administración de análisis (AMO) hace para determinados enlaces:  
  
|Objeto|Enlace|Tipos de datos admitidos|  
|------------|-------------|------------------------|  
|DimensionAttribute|KeyColumns|Todos excepto Binary|  
||NameColumn|Solo WChar|  
||SkippedLevelsColumn|Solo tipos integer: BigInt, Integer, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
||CustomRollupColumn|Solo WChar|  
||CustomRollupPropertiesColumn|Solo WChar|  
||UnaryOperatorColumn|Solo WChar|  
||ValueColumn|All|  
|AttributeTranslation|CaptionColumn|Solo WChar|  
|ScalarMiningStructureColumn|KeyColumns|Todos excepto Binary|  
||NameColumn|Solo WChar|  
|TableMiningStructureColumn|ForeignKeyColumns|Todos excepto Binary|  
|MeasureGroupAttribute|KeyColumns|Todos excepto Binary|  
|Medida de recuento distintiva|Source|BigInt, Currency, Double, Integer, Single, SmallInt, TinyInt, UnsignedBigInt, UnsignedInt, UnsignedSmallInt, UnsignedTinyInt|  
  
  
