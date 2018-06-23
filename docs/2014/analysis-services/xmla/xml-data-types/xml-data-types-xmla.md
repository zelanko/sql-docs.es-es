---
title: Tipos de datos XML (XMLA) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
topic_type:
- apiref
- apinav
helpviewer_keywords:
- XML data types [XMLA]
- data types [XML for Analysis]
- XMLA, data types
- XML for Analysis, data types
ms.assetid: 979b5384-90d9-4e09-9286-1d1eafdc4864
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d7a21691474e890ba8614715b18e972d1353b2c6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36113873"
---
# <a name="xml-data-types-xmla"></a>Tipos de datos XML (XMLA)
  Además de los tipos estándar primitivo y derivado definidos por la recomendación XML 1.0, el XML para las especificaciones de Analysis (XMLA) 1.1 define los tipos de datos adicionales con el fin de admitir la representación de datos multidimensionales y tabulares.  
  
 XMLA utiliza los tipos de datos que aparecen detallados en la siguiente tabla.  
  
|Tipos de datos|Descripción|  
|----------------|-----------------|  
|Boolean|El tipo de datos XML estándar `boolean`.|  
|Decimal|El tipo de datos XML estándar `decimal`.|  
|[EmptyResult](emptyresult-data-type-xmla.md)|Un espacio de nombres en el elemento `root`. Este espacio de nombres se devuelve cuando un comando XMLA no devuelve un resultado debido a que el comando XMLA no devuelve generalmente un resultado o porque se produjo un error en la [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] instancia mientras se ejecuta el comando XMLA.|  
|[EnumString](enumstring-data-type-xmla.md)|Un conjunto de constantes de cadena con nombre para un enumerador determinado.|  
|Integer|El tipo de datos XML estándar `int`.|  
|[MDDataSet](mddataset-data-type-xmla.md)|Datos multidimensionales devueltos por la *resultado* parámetro de la [Execute](../xml-elements-methods-execute.md) método.|  
|[Conjunto de resultados](resultset-data-type-xmla.md)|Un conjunto de resultados XML autodescriptivo devuelto por el método `Execute`.|  
|[Conjunto de filas](rowset-data-type-xmla.md)|Filas de un origen de datos, estructuradas por un esquema XML incrustado, devueltas por la [Discover](../xml-elements-methods-discover.md) método.|  
|String|El tipo de datos XML `string`.|  
|UnsignedInt|El tipo de esquema XML `unsignedInt`.|  
  
 Para conocer las descripciones completas de los tipos de datos XML estándar, vea las recomendaciones candidatas del World Wide Web Consortium (WC3).  
  
## <a name="see-also"></a>Vea también  
 [Elementos XML &#40;XMLA&#41;](../../dev-guide/xml-elements-xmla.md)   
 [XML for Analysis &#40;XMLA&#41; referencia](../xml-for-analysis-xmla-reference.md)  
  
  