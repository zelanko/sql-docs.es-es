---
title: OPENROWSET (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: OPENROWSET
dev_langs: DMX
helpviewer_keywords: OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a95fc508806d4653228caf5a72bac0109646a5f8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;consulta de origen de datos&gt; -OPENROWSET
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Reemplaza la consulta de datos de origen por una consulta a un proveedor externo. Las instrucciones INSERT, SELECT FROM PREDICTION JOIN y SELECT FROM NATURAL PREDICTION JOIN admiten **OPENROWSET**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
OPENROWSET(provider_name,provider_string,query_syntax)  
```  
  
## <a name="arguments"></a>Argumentos  
 *NombreProveedor*  
 Nombre de proveedor OLE DB.  
  
 *provider_string*  
 La cadena de conexión OLE DB para el proveedor especificado.  
  
 *query_syntax*  
 Sintaxis de consulta que devuelve un conjunto de filas.  
  
## <a name="remarks"></a>Comentarios  
 El proveedor de minería de datos, establecerá una conexión con el objeto de origen de datos mediante el uso de *NombreProveedor* y *provider_string,* y se ejecutará la consulta especificada en *query_syntax* para recuperar el conjunto de filas del origen de datos.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo puede usarse en una instrucción PREDICTION JOIN para recuperar datos de la base de datos [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] mediante una instrucción SELECT de [!INCLUDE[tsql](../includes/tsql-md.md)].  
  
```  
OPENROWSET  
(  
'SQLOLEDB.1',  
'Provider=SQLOLEDB.1;Integrated Security=SSPI;Persist Security     Info=False;Initial Catalog=AdventureWorksDW2012;Data Source=localhost',  
'SELECT TOP 1000 * FROM vTargetMail'  
)  
```  
  
## <a name="see-also"></a>Vea también  
 [&#60; consulta de origen de datos &#62;](../dmx/source-data-query.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Instrucciones de manipulación de datos](../dmx/dmx-statements-data-manipulation.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)  
  
  
