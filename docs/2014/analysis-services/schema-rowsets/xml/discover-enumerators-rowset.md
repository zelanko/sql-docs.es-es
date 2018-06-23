---
title: Conjunto de filas DISCOVER_ENUMERATORS | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- DISCOVER_ENUMERATORS
topic_type:
- apiref
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 2c4eb36f93faba7f32352de41d5c6fde4e0dac2c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201462"
---
# <a name="discoverenumerators-rowset"></a>Conjunto de filas DISCOVER_ENUMERATORS
  Devuelve una lista de nombres, tipos de datos y valores de enumeración de enumeradores admitidos por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para un origen de datos concreto. El proveedor de XMLA publica todas las constantes de enumeración que reconoce.  
  
 Si se llama a la [Discover](../../xmla/xml-elements-methods-discover.md) método con el `DISCOVER_ENUMERATORS` valor de enumeración en el [RequestType](../../xmla/xml-elements-properties/type-element-xmla.md) elemento, el `Discover` método devuelve el `DISCOVER_ENUMERATORS` de filas de esquema.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 Para cada enumerador, hay varios elementos, uno para cada valor en la enumeración. El conjunto de filas que representa cada enumerador es plano y el nombre del enumerador se puede repetir para los elementos que pertenecen a la misma enumeración.  
  
 El `DISCOVER_ENUMERATORS` filas contiene las columnas siguientes.  
  
|Nombre de columna|Indicador de tipo|Longitud|Descripción|  
|-----------------|--------------------|------------|-----------------|  
|`EnumName`|`DBTYPE_WSTR`||El nombre del enumerador que contiene un conjunto de valores.|  
|`EnumDescription`|`DBTYPE_WSTR`||Una descripción traducible del enumerador. Puede ser `NULL`.|  
|`EnumType`|`DBTYPE_WSTR`||Tipo de datos subyacente de la enumeración.|  
|`ElementName`|`DBTYPE_WSTR`||Nombre de uno de los elementos de valor en el enumerador establecido.<br /><br /> Ejemplo: `TDP`|  
|`ElementDescription`|`DBTYPE_WSTR`||(Opcional) Una descripción traducible del elemento. Puede ser `NULL`.|  
|`ElementValue`|`DBTYPE_WSTR`||El valor del elemento. Puede ser `NULL`.<br /><br /> Ejemplo: `01`|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El `DISCOVER_ENUMERATORS` se puede restringir el conjunto de filas en las columnas enumeradas en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|`EnumName`|`DBTYPE_WSTR`||  
  
## <a name="see-also"></a>Vea también  
 [Conjuntos de filas de esquema de XML for Analysis](xml-for-analysis-schema-rowsets.md)  
  
  