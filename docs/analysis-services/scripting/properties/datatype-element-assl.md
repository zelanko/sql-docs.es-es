---
title: Elemento DataType (ASSL) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 247d13565e82f2aac4175d262ecfd0f4c94e39b1
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="datatype-element-assl"></a>Elemento DataType (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
|Valor predeterminado|Ninguno|  
|Cardinalidad|0-1: Elemento opcional que puede aparecer solo una vez.|  
  
## <a name="element-relationships"></a>Relaciones del elemento  
  
|Relación|Elemento|  
|------------------|-------------|  
|Elemento primario|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md), [medida](../../../analysis-services/scripting/objects/measure-element-assl.md)|  
|Elementos secundarios|Ninguno|  
  
## <a name="remarks"></a>Comentarios  
 Los valores de **DataType** se definen en el **System.Data.OleDb.OleDbType** enumeración. Sin embargo, solo los valores de enumeración en la tabla siguiente son válidos en el **DataType** elemento.  
  
|Value|Description|  
|-----------|-----------------|  
|*BigInt*|Entero de 64 bits con signo. Este tipo de datos se asigna a la **Int64** tipo de datos en [!INCLUDE[msCoName](../../../includes/msconame-md.md)] tipo de .NET Framework y los datos DBTYPE_I8 en OLE DB.|  
|*BOOL*|Valor booleano. Este tipo de datos se asigna a la **booleano** tipo de datos de .NET Framework y el tipo de datos DBTYPE_BOOL en OLE DB.|  
|*Moneda*|Un valor de moneda comprendido entre -2<sup>63</sup> (o -922.337.203.685.477,5808) a 2<sup>63</sup>-1 (o + 922.337.203.685.477,5807) con una precisión de una diezmilésima de unidad de moneda. Este tipo de datos se asigna a la **Decimal** tipo de datos de .NET Framework y el tipo de datos DBTYPE_CY en OLE DB.|  
|*Date*|Fecha de los datos, almacenada como un número de punto flotante de precisión doble. La parte entera es el número de días transcurridos desde el 30 de diciembre de 1899 y la parte decimal es una fracción del día. Este tipo de datos se asigna a la **DateTime** tipo de datos de .NET Framework y el tipo de datos DBTYPE_DATE en OLE DB.|  
|*Doble*|Número de punto flotante de precisión doble en el intervalo de -1,79E +308 a 1,79E +308. Este tipo de datos se asigna a la **doble** tipo de datos de .NET Framework y el tipo de datos DBTYPE_R8 en OLE DB.|  
|*Integer*|Entero de 32 bits con signo. Este tipo de datos se asigna a la **Int32** tipo de datos de .NET Framework y el tipo de datos DBTYPE_I4 en OLE DB.|  
|*Único*|Un número de punto flotante de precisión simple en el intervalo de -3,40E +38 a 3,40E +38. Este tipo de datos se asigna a la **único** tipo de datos de .NET Framework y el tipo de datos DBTYPE_R4 en OLE DB.|  
|*SmallInt*|Entero de 16 bits con signo. Este tipo de datos se asigna a la **Int16** tipo de datos de .NET Framework y el tipo de datos DBTYPE_I2 en OLE DB.|  
|*TinyInt*|Entero de 8 bits con signo. Este tipo de datos se asigna a la **SByte** tipo de datos de .NET Framework y el tipo de datos DBTYPE_I1 en OLE DB.|  
|*UnsignedBigInt*|Entero de 64 bits sin signo. Este tipo de datos se asigna a la **UInt64** tipo de datos de .NET Framework y el tipo de datos DBTYPE_UI8 en OLE DB.|  
|*UnsignedInt*|Entero de 32 bits sin signo. Este tipo de datos se asigna a la **UInt32** tipo de datos de .NET Framework y el tipo de datos DBTYPE_UI4 en OLE DB.|  
|*UnsignedSmallInt*|Entero de 16 bits sin signo. Este tipo de datos se asigna a la **UInt16** tipo de datos de .NET Framework y el tipo de datos DBTYPE_UI2 en OLE DB.|  
|*WChar*|Flujo de caracteres Unicode terminado en NULL. Este tipo de datos se asigna a la **cadena** tipo de datos de .NET Framework y el tipo de datos DBTYPE_WSTR en OLE DB.|  
|*Heredado*|Tipo de datos de la **DataItem** contenidos en el [origen](../../../analysis-services/scripting/properties/source-element-measure-assl.md) elemento de la **medida** elemento.<br /><br /> Nota: Solo es aplicable a **medida** elementos.|  
  
## <a name="see-also"></a>Vea también  
 [Propiedades & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
