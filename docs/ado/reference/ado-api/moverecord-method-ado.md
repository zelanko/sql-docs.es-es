---
title: "Método MoveRecord (ADO) | Documentos de Microsoft"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f385fc1fd6c7374a9d693d8fcb898f817c54bbc7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="moverecord-method-ado"></a>Método MoveRecord (ADO)
Mueve la entidad representada por un [registro](../../../ado/reference/ado-api/record-object-ado.md) a otra ubicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. A **cadena** valor que contiene una dirección URL identifica el **registro** va a mover. Si *origen* se omite o se especifica una cadena vacía, el objeto representado por este **registro** se mueve. Por ejemplo, si la **registro** representa un archivo, el contenido del archivo se mueve a la ubicación especificada por *destino*.  
  
 *Destino*  
 Opcional. A **cadena** valor que contiene la dirección URL que especifica la ubicación donde *origen* se va a mover.  
  
 *UserName*  
 Opcional. A **cadena** valor que contiene el identificador de usuario que, si es necesario, autoriza el acceso a *destino*.  
  
 *Contraseña*  
 Opcional. A **cadena** que contiene la contraseña que comprueba si es necesario, *nombre de usuario*.  
  
 *Opciones*  
 Opcional. A [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) valor cuyo valor predeterminado es **adMoveUnspecified**. Especifica el comportamiento de este método.  
  
 *Async*  
 Opcional. A **booleano** valor que, cuando **True**, especifica que esta operación debe ser asincrónica.  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** valor. Normalmente, el valor de *destino* se devuelve. Sin embargo, el valor devuelto exacto depende del proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de *origen* y *destino* no debe ser idéntico; en caso contrario, se produce un error de tiempo de ejecución. Al menos los nombres de servidor, la ruta de acceso y el recurso deben ser diferente.  
  
 Para los archivos transferidos mediante el proveedor de publicación en Internet, este método actualiza todos los vínculos de hipertexto de archivos que se mueven a menos que se especifique lo contrario en *opciones*. Este método produce un error si *destino* identifica un objeto existente (por ejemplo, un archivo o directorio), a menos que **adMoveOverWrite** se especifica.  
  
> [!NOTE]
>  Use la **adMoveOverWrite** opción con prudencia. Por ejemplo, especificar esta opción para mover un archivo a un directorio eliminará el directorio y reemplazarlo con el archivo.  
  
 Algunos atributos de la **registro** objeto, como el [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propiedad, no se actualizará cuando se complete esta operación. Actualizar el **registro** propiedades del objeto cerrando la **registro**, a continuación, vuelva a abrirlo con la dirección URL de la ubicación donde se ha movido el archivo o directorio.  
  
 Si este **registro** se obtuvo de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), la nueva ubicación del directorio o archivo movido no se reflejará inmediatamente en el **conjunto de registros**. Actualizar el **Recordset** al cerrar y volver a abrirlo.  
  
> [!NOTE]
>  Direcciones URL que utilizan el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para Internet Publishing](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de registro (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Move (método) (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)

