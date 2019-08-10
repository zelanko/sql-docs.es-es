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
ms.openlocfilehash: caac43eb176e17a6e92e487f3dedae71a252f5af
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68887725"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta&gt; de datos de origen: OPENQUERY
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Reemplaza la consulta de datos de origen por una consulta a un origen de datos existente. Las instrucciones INSERT, SELECT FROM predicción JOIN y SELECT FROM NATURAL PREDICT JOIN admiten **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *DataSource con nombre*  
 Origen de datos que existe en la [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos.  
  
 *Sintaxis de consulta*  
 Sintaxis de consulta que devuelve un conjunto de filas.  
  
## <a name="remarks"></a>Comentarios  
 **OPENQUERY** proporciona una manera más segura de acceder a los datos externos mediante la compatibilidad con los permisos del origen de datos. La cadena de conexión se almacena en el origen de datos, lo que permite a los administradores utilizar las propiedades del origen de datos para administrar el acceso a los mismos. Para obtener más información sobre los orígenes de datos, vea [orígenes &#40;de datos compatibles SSAS&#41;-multidimensional](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional).  
  
 Puede obtener una lista de los orígenes de datos que están disponibles en un servidor consultando el conjunto de filas de esquema **MDSCHEMA_INPUT_DATASOURCES** . Para obtener más información sobre el uso de **MDSCHEMA_INPUT_DATASOURCES**, vea [conjunto de filas MDSCHEMA_INPUT_DATASOURCES](https://docs.microsoft.com/bi-reference/schema-rowsets/ole-db-olap/mdschema-input-datasources-rowset).  
  
 También puede devolver una lista de orígenes de datos en la base de datos de Analysis Services actual utilizando la consulta DMX siguiente:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el origen de datos MyDS ya [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] definido en la base de datos para [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] crear una conexión a la base de datos y consultar la vista **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Vea también  
 [&#60;consulta de datos de origen&#62;](../dmx/source-data-query.md)   
 [Instrucciones de manipulación &#40;de&#41; datos DMX de extensiones de minería de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
