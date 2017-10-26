---
title: OPENROWSET (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- OPENROWSET
dev_langs:
- DMX
helpviewer_keywords:
- OPENROWSET statement
ms.assetid: 8c8b61b4-2bf6-46c7-8976-51484004dc22
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 914e1be70255414373fd758301ef0682f3aba6e7
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="ltsource-data-querygt---openrowset"></a>&lt;consulta de origen de datos&gt; -OPENROWSET
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

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
  
  

