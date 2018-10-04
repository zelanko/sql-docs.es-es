---
title: DeleteRecord (método, ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_DeleteRecord
- _Record::DeleteRecord
helpviewer_keywords:
- DeleteRecord method [ADO]
ms.assetid: 2726498c-dbd8-4266-983b-ae7d62c39142
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 23c66eb3ca786df27f856539e8bba026d2b1ea71
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47674122"
---
# <a name="deleterecord-method-ado"></a>DeleteRecord (método, ADO)
Elimina una entidad representada por un [registro](../../../ado/reference/ado-api/record-object-ado.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Record.DeleteRecord Source, Async  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. Un **cadena** valor que contiene una dirección URL que identifica la entidad (por ejemplo, el archivo o directorio) va a eliminar. Si *origen* se omite o se especifica una cadena vacía, la entidad representada por el actual [registro](../../../ado/reference/ado-api/record-object-ado.md) se elimina. Si el registro es una colección ([RecordType](../../../ado/reference/ado-api/recordtype-property-ado.md) de **es adCollectionRecord**, por ejemplo, un directorio) también se eliminarán todos los elementos secundarios (por ejemplo, subdirectorios).  
  
 *Async*  
 Opcional. Un **booleano** valor que, cuando **True**, especifica que la operación de eliminación es asincrónico.  
  
## <a name="remarks"></a>Comentarios  
 Operaciones en el objeto representado por este **registro** puede producir un error cuando este método finalice. Después de llamar a **DeleteRecord**, **registro** debe estar cerrado porque el comportamiento de la **registro** pueden llegar a ser impredecible dependiendo de cuándo se actualiza el proveedor de la **Registro** con el origen de datos.  
  
 Si este **registro** se obtuvo de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), a continuación, los resultados de esta operación no se reflejarán inmediatamente en el **conjunto de registros**. Actualizar el **Recordset** al cerrar y volver a abrirlo, o mediante la ejecución de la **Recordset** [Requery](../../../ado/reference/ado-api/requery-method.md) método, el [actualización](../../../ado/reference/ado-api/update-method.md) método, o el [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [El método Delete (colección Fields de ADO)](../../../ado/reference/ado-api/delete-method-ado-fields-collection.md)   
 [Método Delete (colección de parámetros de ADO)](../../../ado/reference/ado-api/delete-method-ado-parameters-collection.md)   
 [Delete (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/delete-method-ado-recordset.md)
