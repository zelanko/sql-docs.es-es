---
title: OPENQUERY (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- OPENQUERY
dev_langs:
- DMX
helpviewer_keywords:
- OPENQUERY statement
ms.assetid: fe57f3a3-a8e6-402c-995e-bd2fe28a7a7c
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6e8c250b96c2da83e6dd34263ccddeb622a67050
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta de origen de datos&gt; -OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Reemplaza la consulta de datos de origen por una consulta a un origen de datos existente. Las instrucciones INSERT, SELECT FROM PREDICTION JOIN y SELECT FROM NATURAL PREDICTION JOIN admiten **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *origen de datos con nombre*  
 Un origen de datos que existe en el [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos.  
  
 *sintaxis de consulta*  
 Sintaxis de consulta que devuelve un conjunto de filas.  
  
## <a name="remarks"></a>Notas  
 **OPENQUERY** proporciona una forma más segura para tener acceso a datos externos por compatibilidad con los permisos de origen de datos. La cadena de conexión se almacena en el origen de datos, lo que permite a los administradores utilizar las propiedades del origen de datos para administrar el acceso a los mismos. Para obtener más información acerca de los orígenes de datos, vea [admite orígenes de datos &#40; SSAS - Multidimensional &#41; ](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 Puede obtener una lista de los orígenes de datos que están disponibles en un servidor consultando la **MDSCHEMA_INPUT_DATASOURCES** de filas de esquema. Para obtener más información sobre el uso de **MDSCHEMA_INPUT_DATASOURCES**, consulte [de filas MDSCHEMA_INPUT_DATASOURCES](../analysis-services/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset.md).  
  
 También puede devolver una lista de orígenes de datos en la base de datos de Analysis Services actual utilizando la consulta DMX siguiente:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se utiliza el origen de datos MyDS ya definido en el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos para crear una conexión a la [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] base de datos y consulta el **vTargetMail** vista.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Ver también  
 [&#60; consulta de origen de datos &#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
