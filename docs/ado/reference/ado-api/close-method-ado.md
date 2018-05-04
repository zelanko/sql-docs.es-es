---
title: Close (método) (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::Close
- _Stream::Close
- _Record::Close
helpviewer_keywords:
- Close method [ADO]
ms.assetid: 3cdf27d1-a180-4cff-8e42-95dec5fb1b55
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a88b6eefe8e251d97bbc77fbcdd3a7b2dc911983
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="close-method-ado"></a>Close (método) (ADO)
Cierra un objeto abierto y los objetos dependientes.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
object.Close  
```  
  
## <a name="remarks"></a>Comentarios  
 Use la **cerrar** método para cerrar un [conexión](../../../ado/reference/ado-api/connection-object-ado.md), un [registro](../../../ado/reference/ado-api/record-object-ado.md), un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), o un [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto para liberar los recursos del sistema asociados. Cerrar un objeto no se quita de la memoria; puede cambiar sus valores de propiedad y abrirlo de nuevo más tarde. Para eliminar completamente un objeto de la memoria, cierre el objeto y, a continuación, establezca la variable de objeto en *nada* (en Visual Basic).  
  
## <a name="connection"></a>Conexión  
 Mediante el **cerrar** método para cerrar un **conexión** objeto también cierra cualquier activo **Recordset** objetos asociados con la conexión. A [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto asociado a la **conexión** objeto que está cerrando persistirá, pero que ya no se puede asociar con un **conexión** objeto; es decir, su [ ActiveConnection](../../../ado/reference/ado-api/activeconnection-property-ado.md) propiedad se establecerá en **nada**. Además, el **comando** del objeto [parámetros](../../../ado/reference/ado-api/parameters-collection-ado.md) se borrará la colección de los parámetros definidos por el proveedor.  
  
 Posteriormente, podrá llamar el [abiertos](../../../ado/reference/ado-api/open-method-ado-connection.md) método para volver a establecer la conexión con el mismo u otro origen de datos. Mientras el **conexión** objeto está cerrado, llamar a cualquier método que requiera una conexión abierta con el origen de datos genera un error.  
  
 Cerrar un **conexión** objeto mientras hay abierto **Recordset** objetos en la conexión se deshacen los cambios pendientes en todos los **Recordset** objetos. Cerrar explícitamente una **conexión** objeto (una llamada a la **cerrar** método) mientras la transacción está en curso, generará un error. Si un **conexión** objeto queda fuera del ámbito mientras hay una transacción está en curso, ADO deshace automáticamente la transacción.  
  
## <a name="recordset-record-stream"></a>Conjunto de registros, registro, flujo  
 Mediante el **cerrar** método para cerrar un **Recordset**, **registro**, o **flujo** objeto libera los datos asociados y cualquier acceso exclusivo Puede que haya tenido a los datos a través de este objeto en concreto. Posteriormente, podrá llamar el [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md) atributos de método para volver a abrir el objeto con el mismo o modificada.  
  
 Mientras un **Recordset** objeto está cerrado, llamar a cualquier método que requiera un cursor activo genera un error.  
  
 Si es una operación de edición en curso mientras esté en modo de actualización inmediata, la llamada a la **cerrar** método genera un error; en su lugar, llame a la [actualizar](../../../ado/reference/ado-api/update-method.md) o [CancelUpdate](../../../ado/reference/ado-api/cancelupdate-method-ado.md) método primero. Si cierra el **Recordset** objeto mientras esté en modo de actualización por lotes, todos los cambios desde la última [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) llamada se pierden.  
  
 Si usas el [clon](../../../ado/reference/ado-api/clone-method-ado.md) método para crear copias de un formato de archivo **Recordset** objeto, cierra el original o un clon no afecta a cualquiera de las demás copias.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)|[Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de los métodos de apertura y cierre (VB)](../../../ado/reference/ado-api/open-and-close-methods-example-vb.md)   
 [Ejemplo de los métodos de apertura y cierre (VBScript)](../../../ado/reference/ado-api/open-and-close-methods-example-vbscript.md)   
 [Ejemplo de los métodos de apertura y cierre (VC ++)](../../../ado/reference/ado-api/open-and-close-methods-example-vc.md)   
 [Open (método) (conexión de ADO)](../../../ado/reference/ado-api/open-method-ado-connection.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Save (método)](../../../ado/reference/ado-api/save-method.md)
