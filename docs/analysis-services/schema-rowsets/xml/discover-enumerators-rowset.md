---
title: Conjunto de filas DISCOVER_ENUMERATORS | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- DISCOVER_ENUMERATORS
apitype: NA
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_ENUMERATORS rowset
ms.assetid: ddc7b13c-3135-4419-8166-eddd459167da
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 2a1d5135a421ab691e9801f652aca47108a64af7
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="discoverenumerators-rowset"></a>Conjunto de filas DISCOVER_ENUMERATORS
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Devuelve una lista de nombres, tipos de datos y valores de enumeración de enumeradores admitidos por el proveedor de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] XML for Analysis (XMLA) para un origen de datos concreto. El proveedor de XMLA publica todas las constantes de enumeración que reconoce.  
  
 Si se llama a la [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) método con el **DISCOVER_ENUMERATORS** valor de enumeración en el [RequestType](../../../analysis-services/xmla/xml-elements-properties/requesttype-element-xmla.md) elemento, el **Discover** método devuelve el **DISCOVER_ENUMERATORS** de filas de esquema.  
  
## <a name="rowset-columns"></a>Columnas del conjunto de filas  
 Para cada enumerador, hay varios elementos, uno para cada valor en la enumeración. El conjunto de filas que representa cada enumerador es plano y el nombre del enumerador se puede repetir para los elementos que pertenecen a la misma enumeración.  
  
 El conjunto de filas **DISCOVER_ENUMERATORS** contiene las siguientes columnas.  
  
|Nombre de columna|Indicador de tipo|Longitud|Description|  
|-----------------|--------------------|------------|-----------------|  
|**Nombredeenumeración**|**DBTYPE_WSTR**||El nombre del enumerador que contiene un conjunto de valores.|  
|**EnumDescription**|**DBTYPE_WSTR**||Una descripción traducible del enumerador. Puede ser **NULL**.|  
|**EnumType**|**DBTYPE_WSTR**||Tipo de datos subyacente de la enumeración.|  
|**ElementName**|**DBTYPE_WSTR**||Nombre de uno de los elementos de valor en el enumerador establecido.<br /><br /> Ejemplo: **TDP**|  
|**ElementDescription**|**DBTYPE_WSTR**||(Opcional) Una descripción traducible del elemento. Puede ser **NULL**.|  
|**ElementValue**|**DBTYPE_WSTR**||El valor del elemento. Puede ser **NULL**.<br /><br /> Ejemplo: **01**|  
  
 Este conjunto de filas de esquema no está ordenado.  
  
## <a name="restriction-columns"></a>Columnas de restricción  
 El conjunto de filas **DISCOVER_ENUMERATORS** puede tener restricciones en las columnas que se muestran en la tabla siguiente.  
  
|Nombre de columna|Indicador de tipo|Estado de restricción|  
|-----------------|--------------------|-----------------------|  
|**Nombredeenumeración**|**DBTYPE_WSTR**||  
  
## <a name="see-also"></a>Vea también  
 [XML para conjuntos de filas de esquema de análisis](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
