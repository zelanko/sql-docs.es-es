---
title: OPENQUERY (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a075f314af0eb8ea2eb0bc941ada0bc38e22fec3
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970435"
---
# <a name="ltsource-data-querygt---openquery"></a>&lt;consulta de datos &gt; de origen: OPENQUERY
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  Reemplaza la consulta de datos de origen por una consulta a un origen de datos existente. Las instrucciones INSERT, SELECT FROM predicción JOIN y SELECT FROM NATURAL PREDICT JOIN admiten **OPENQUERY**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENQUERY(<named datasource>, <query syntax>)  
```  
  
## <a name="arguments"></a>Argumentos  
 *DataSource con nombre*  
 Origen de datos que existe en la base de datos [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 *Sintaxis de consulta*  
 Sintaxis de consulta que devuelve un conjunto de filas.  
  
## <a name="remarks"></a>Observaciones  
 **OPENQUERY** proporciona una manera más segura de acceder a los datos externos mediante la compatibilidad con los permisos del origen de datos. La cadena de conexión se almacena en el origen de datos, lo que permite a los administradores utilizar las propiedades del origen de datos para administrar el acceso a los mismos. Para obtener más información sobre los orígenes de datos, vea [orígenes de datos compatibles &#40;SSAS-multidimensional&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional).  
  
 Puede obtener una lista de los orígenes de datos que están disponibles en un servidor consultando el conjunto de filas de esquema **MDSCHEMA_INPUT_DATASOURCES** . Para obtener más información sobre el uso de **MDSCHEMA_INPUT_DATASOURCES**, vea [MDSCHEMA_INPUT_DATASOURCES conjunto de filas](https://docs.microsoft.com/previous-versions/sql/sql-server-2012/ms126243(v=sql.110)).  
  
 También puede devolver una lista de orígenes de datos en la base de datos de Analysis Services actual utilizando la consulta DMX siguiente:  
  
 `SELECT * FROM $system.MDSCHEMA_INPUT_DATASOURCES`  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa el origen de datos MyDS ya definido en la base de datos [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para crear una conexión a la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] y consultar la vista **vTargetMail** .  
  
```  
OPENQUERY (MyDS,'SELECT TOP 1000 * FROM vTargetMail')  
```  
  
## <a name="see-also"></a>Consulte también  
 [&#60;consulta de datos de origen&#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40;DMX&#41; instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Referencia de instrucciones de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
