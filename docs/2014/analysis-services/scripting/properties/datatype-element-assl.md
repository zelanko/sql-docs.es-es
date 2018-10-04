---
title: Elemento DataType (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DataType Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataType
helpviewer_keywords:
- DataType element
ms.assetid: efe6f717-8288-4ca2-85ed-9b63d27c02d8
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 92c3981344d0425c46ef283fa8792de942d6193b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48191045"
---
# <a name="datatype-element-assl"></a>Elemento DataType (ASSL)
  Define el tipo de datos del elemento asociado.  
  
## <a name="syntax"></a>Sintaxis  
  
```xml  
  
<DataItem> <!-- or Measure -->  
   ...  
   <DataType>...</DataType>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>Características de los elementos  
  
|Característica|Descripción|  
|--------------------|-----------------|  
|Tipo y longitud de los datos|String (enumeración)|  
|Valor predeterminado|None|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer una y solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DataItem](../data-type/dataitem-data-type-assl.md), [medida](../objects/measure-element-assl.md)|  
|Elementos secundarios|None|  
  
## <a name="remarks"></a>Comentarios  
 Los valores de `DataType` se definen en la enumeración `System.Data.OleDb.OleDbType`. Sin embargo, solo los valores de enumeración de la tabla siguiente son válidos en el elemento `DataType`.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|*BigInt*|Entero de 64 bits con signo. Este tipo de datos se asigna a la `Int64` tipo de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipo de .NET Framework y los datos DBTYPE_I8 en OLE DB.|  
|*BOOL*|Valor Boolean. Este tipo de datos se asigna al tipo de datos `Boolean` en .NET Framework y al tipo de datos DBTYPE_BOOL en OLE DB.|  
|*Moneda*|Un valor de moneda comprendido entre -2<sup>63</sup> (o -922.337.203.685.477,5808) a 2<sup>63</sup>-1 (o + 922.337.203.685.477,5807) con una precisión de una diezmilésima de unidad de moneda. Este tipo de datos se asigna al tipo de datos `Decimal` en .NET Framework y al tipo de datos DBTYPE_CY en OLE DB.|  
|*Date*|Fecha de los datos, almacenada como un número de punto flotante de precisión doble. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción del día. Este tipo de datos se asigna al tipo de datos `DateTime` en .NET Framework y al tipo de datos DBTYPE_DATE en OLE DB.|  
|*Doble*|Número de punto flotante de precisión doble en el intervalo de -1,79E +308 a 1,79E +308. Este tipo de datos se asigna al tipo de datos `Double` en .NET Framework y al tipo de datos DBTYPE_R8 en OLE DB.|  
|*Integer*|Entero de 32 bits con signo. Este tipo de datos se asigna al tipo de datos `Int32` en .NET Framework y al tipo de datos DBTYPE_I4 en OLE DB.|  
|*Único*|Un número de punto flotante de precisión simple en el intervalo de -3,40E +38 a 3,40E +38. Este tipo de datos se asigna al tipo de datos `Single` en .NET Framework y al tipo de datos DBTYPE_R4 en OLE DB.|  
|*SmallInt*|Entero de 16 bits con signo. Este tipo de datos se asigna al tipo de datos `Int16` en .NET Framework y al tipo de datos DBTYPE_I2 en OLE DB.|  
|*TinyInt*|Entero de 8 bits con signo. Este tipo de datos se asigna al tipo de datos `SByte` en .NET Framework y al tipo de datos DBTYPE_I1 en OLE DB.|  
|*UnsignedBigInt*|Entero de 64 bits sin signo. Este tipo de datos se asigna al tipo de datos `UInt64` en .NET Framework y al tipo de datos DBTYPE_UI8 en OLE DB.|  
|*UnsignedInt*|Entero de 32 bits sin signo. Este tipo de datos se asigna al tipo de datos `UInt32` en .NET Framework y al tipo de datos DBTYPE_UI4 en OLE DB.|  
|*UnsignedSmallInt*|Entero de 16 bits sin signo. Este tipo de datos se asigna al tipo de datos `UInt16` en .NET Framework y al tipo de datos DBTYPE_UI2 en OLE DB.|  
|*WChar*|Flujo de caracteres Unicode terminado en NULL. Este tipo de datos se asigna al tipo de datos `String` en .NET Framework y al tipo de datos DBTYPE_WSTR en OLE DB.|  
|*Heredado*|Tipo de datos de la `DataItem` contenidos en el [origen](source-element-measure-assl.md) elemento de la `Measure` elemento. **Nota:** aplicable únicamente a `Measure` elementos.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades &#40;ASSL&#41;](properties-assl.md)  
  
  
