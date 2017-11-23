---
title: ExecuteOptionEnum | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: ExecuteOptionEnum
helpviewer_keywords: ExecuteOptionEnum enumeration [ADO]
ms.assetid: 68bfa83a-5df4-4bef-8736-0f88ae8c29ea
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8357988f5082498114c435f899e898552fca1707
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="executeoptionenum"></a>ExecuteOptionEnum
Especifica cómo un proveedor debe ejecutar un comando.  
  
|Constante|Valor|Description|  
|--------------|-----------|-----------------|  
|**adAsyncExecute**|0x10|Indica que el comando debería ejecutarse de forma asincrónica.<br /><br /> Este valor no puede combinarse con la [CommandTypeEnum](../../../ado/reference/ado-api/commandtypeenum.md) valor **adCmdTableDirect**.|  
|**adAsyncFetch**|0x20|Indica que las filas restantes después de la cantidad inicial especificado en el [CacheSize](../../../ado/reference/ado-api/cachesize-property-ado.md) propiedad se debe recuperar de forma asincrónica.|  
|**adAsyncFetchNonBlocking**|0x40|Indica que el subproceso principal nunca se bloquea durante la recuperación. Si la fila solicitada no se ha recuperado, la fila actual se desplaza automáticamente hasta el final del archivo.<br /><br /> Si abre un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) desde una [flujo](../../../ado/reference/ado-api/stream-object-ado.md) que contiene una forma persistente almacenado **Recordset**, **adAsyncFetchNonBlocking** no tendrá un efecto; la operación será sincrónica y de bloqueo.<br /><br /> **adAsynchFetchNonBlocking** no tiene ningún efecto cuando la [adCmdTableDirect](../../../ado/reference/ado-api/commandtypeenum.md) opción se utiliza para abrir el **conjunto de registros**.|  
|**adExecuteNoRecords**|0x80|Indica que el texto del comando es un comando o procedimiento almacenado que no devuelve filas (por ejemplo, un comando que sólo inserta datos). Si se recuperan todas las filas, se descartan y no devuelve.<br /><br /> **adExecuteNoRecords** solo se pueden pasar como un parámetro opcional para el **comando** o **conexión ejecute** método.|  
|**adExecuteStream**|0x400|Indica que se deben devolver los resultados de una ejecución de comandos como una secuencia.<br /><br /> **adExecuteStream** solo se pueden pasar como un parámetro opcional para el **ejecutar comando** método.|  
|**adExecuteRecord**||Indica que la **CommandText** es un comando o procedimiento almacenado que devuelve una sola fila que se debe devolver como un **registro** objeto.|  
|**realiza la consulta**|-1|Indica que el comando no está especificado.|  
  
## <a name="adowfc-equivalent"></a>Equivalente ADO/WFC  
 Paquete: **com.ms.wfc.data**  
  
|Constante|  
|--------------|  
|AdoEnums.ExecuteOption.ASYNCEXECUTE|  
|AdoEnums.ExecuteOption.ASYNCFETCH|  
|AdoEnums.ExecuteOption.ASYNCFETCHNONBLOCKING|  
|AdoEnums.ExecuteOption.NORECORDS|  
|AdoEnums.ExecuteOption.UNSPECIFIED|  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Método Execute (Command ADO)](../../../ado/reference/ado-api/execute-method-ado-command.md)|[Execute (método) (conexión de ADO)](../../../ado/reference/ado-api/execute-method-ado-connection.md)|  
|[Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)|[Requery (método)](../../../ado/reference/ado-api/requery-method.md)|
