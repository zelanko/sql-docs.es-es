---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 895c28f0989debb899c1e01c80a18483d3cda5a1
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147820"
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
  
## <a name="remarks"></a>Comentarios  
 **OPENQUERY** proporciona una forma más segura para tener acceso a datos externos mediante la compatibilidad con los permisos de origen de datos. La cadena de conexión se almacena en el origen de datos, lo que permite a los administradores utilizar las propiedades del origen de datos para administrar el acceso a los mismos. Para obtener más información acerca de los orígenes de datos, vea [orígenes de datos admitidos &#40;SSAS - multidimensionales&#41;](../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md).  
  
 Puede obtener una lista de los orígenes de datos que están disponibles en un servidor consultando la **MDSCHEMA_INPUT_DATASOURCES** de filas de esquema. Para obtener más información sobre el uso de **MDSCHEMA_INPUT_DATASOURCES**, consulte [de filas MDSCHEMA_INPUT_DATASOURCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset).  
  
 También puede devolver una lista de orígenes de datos en la base de datos de Analysis Services actual utilizando la consulta DMX siguiente:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el origen de datos MyDS ya definido en el [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos para crear una conexión a la [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] base de datos y consulta el **vTargetMail** vista.  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Vea también  
 [&#60;consulta de origen de datos&#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
