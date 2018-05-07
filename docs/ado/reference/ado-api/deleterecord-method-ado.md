---
title: Método DeleteRecord (ADO) | Documentos de Microsoft
ms.prod: sql
ms.prod_service: connectivity
ms.component: ado
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ca7b2a425e24a115b8572f26ec7b2efb103ba9ec
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="deleterecord-method-ado"></a>DeleteRecord (método, ADO)
Elimina una entidad representada por un [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. A **cadena** valor que contiene una dirección URL que identifica la entidad (por ejemplo, el archivo o directorio) va a eliminar. Si *origen* se omite o se especifica una cadena vacía, la entidad representada por el actual [registro](../../../ado/reference/ado-api/record-object-ado.md) se elimina. Si el registro es una colección ([Tiporegistro](../../../ado/reference/ado-api/recordtype-property-ado.md) de **es adCollectionRecord**, como un directorio) también se eliminarán todos los elementos secundarios (por ejemplo, subdirectorios).  
  
 *Async*  
 Opcional. A **booleano** valor que, cuando **True**, especifica que la operación de eliminación es asincrónico.  
  
## <a name="remarks"></a>Comentarios  
 Operaciones en el objeto representado por este **registro** puede producir un error cuando este método finalice. Después de llamar a **DeleteRecord**, el **registro** debe estar cerrado porque el comportamiento de la **registro** quede imprevisible según cuando se actualiza el proveedor de la **Registro** con el origen de datos.  
  
 Si este **registro** se obtuvo de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), a continuación, los resultados de esta operación no se reflejarán inmediatamente en el **conjunto de registros**. Actualizar el **Recordset** al cerrar y volver a abrirlo, o mediante la ejecución de la **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) método, el [actualización](../../../ado/reference/ado-api/update-method.md) método, o el [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
