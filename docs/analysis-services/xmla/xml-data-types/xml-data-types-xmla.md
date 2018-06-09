---
title: Tipos de datos XML (XMLA) | Documentos de Microsoft
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: c52717a6f061f4708b2d3e46c6d34f837b2039af
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/04/2018
ms.locfileid: "34573787"
---
# <a name="xml-data-types-xmla"></a>Tipos de datos XML (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  Además de los tipos estándar primitivo y derivado definidos por la recomendación XML 1.0, el XML para las especificaciones de Analysis (XMLA) 1.1 define los tipos de datos adicionales con el fin de admitir la representación de datos multidimensionales y tabulares.  
  
 XMLA utiliza los tipos de datos que aparecen detallados en la siguiente tabla.  
  
|Tipos de datos|Descripción|  
|----------------|-----------------|  
|Boolean|El tipo de datos XML estándar **boolean** .|  
|Decimal|El tipo de datos XML estándar **decimal** .|  
|[EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|Un espacio de nombres en el elemento **root** . Este espacio de nombres se devuelve cuando un comando XMLA no devuelve un resultado debido a que el comando XMLA no devuelve generalmente un resultado o porque se produjo un error en la instancia de Analysis Services al ejecutar el comando XMLA.|  
|[EnumString](../../../analysis-services/xmla/xml-data-types/enumstring-data-type-xmla.md)|Un conjunto de constantes de cadena con nombre para un enumerador determinado.|  
|Integer|El tipo de datos XML estándar **int** .|  
|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)|Datos multidimensionales devueltos por la *resultado* parámetro de la [Execute](../../../analysis-services/xmla/xml-elements-methods-execute.md) método.|  
|[Conjunto de resultados](../../../analysis-services/xmla/xml-data-types/resultset-data-type-xmla.md)|Un conjunto de resultados XML autodescriptivo devuelto por el método **Execute** .|  
|[Conjunto de filas](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)|Filas de un origen de datos, estructuradas por un esquema XML incrustado, devueltas por la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método.|  
|String|El tipo de datos XML **string** .|  
|UnsignedInt|El tipo de esquema XML **unsignedInt** .|  
  
 Para conocer las descripciones completas de los tipos de datos XML estándar, vea las recomendaciones candidatas del World Wide Web Consortium (WC3).  
  
## <a name="see-also"></a>Vea también
 [Elementos XML &#40;XMLA&#41;](http://msdn.microsoft.com/library/40ab2360-efb6-4ba6-bf23-e84964e51008)   
 [XML for Analysis &#40;XMLA&#41; referencia](../../../analysis-services/xmla/xml-for-analysis-xmla-reference.md)  
  
  
