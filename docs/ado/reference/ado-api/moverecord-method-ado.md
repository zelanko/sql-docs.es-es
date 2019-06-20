---
title: Método MoveRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::MoveRecord
- _Record::raw_MoveRecord
helpviewer_keywords:
- MoveRecord method [ADO]
ms.assetid: 6d2807b0-b861-4583-bcaf-fb0b82e0f2d0
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: fe9dc770f537b9b9f8b53461c30b890a4144a821
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66707346"
---
# <a name="moverecord-method-ado"></a>Método MoveRecord (ADO)
Mueve la entidad representada por un [registro](../../../ado/reference/ado-api/record-object-ado.md) a otra ubicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Record.MoveRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. Un **cadena** valor que contiene una dirección URL que identifica el **registro** va a mover. Si *origen* se omite o se especifica una cadena vacía, el objeto representado por este **registro** se mueve. Por ejemplo, si la **registro** representa un archivo, el contenido del archivo se mueve a la ubicación especificada por *destino*.  
  
 *Destino*  
 Opcional. Un **cadena** valor que contiene la dirección URL que especifica la ubicación donde *origen* se va a mover.  
  
 *UserName*  
 Opcional. Un **cadena** valor que contiene el identificador de usuario que, si es necesario, autoriza el acceso a *destino*.  
  
 *Contraseña*  
 Opcional. Un **cadena** que contiene la contraseña que, si es necesario, comprueba *UserName*.  
  
 *Opciones*  
 Opcional. Un [MoveRecordOptionsEnum](../../../ado/reference/ado-api/moverecordoptionsenum.md) cuyo valor predeterminado es el valor **adMoveUnspecified**. Especifica el comportamiento de este método.  
  
 *Async*  
 Opcional. Un **booleano** valor que, cuando **True**, especifica que esta operación debe ser asincrónica.  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **String**. Normalmente, el valor de *destino* se devuelve. Sin embargo, el valor devuelto exacto depende del proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de *origen* y *destino* no debe ser idéntico; en caso contrario, se produce un error de tiempo de ejecución. Al menos los nombres de servidor, la ruta de acceso y el recurso deben ser diferente.  
  
 Para los archivos movidos mediante el proveedor de publicación en Internet, este método actualiza todos los vínculos de hipertexto de los archivos que se va a mover a menos que especifique otra cosa *opciones*. Este método produce un error si *destino* identifica un objeto existente (por ejemplo, un archivo o directorio), a menos que **adMoveOverWrite** se especifica.  
  
> [!NOTE]
>  Use la **adMoveOverWrite** opción con prudencia. Por ejemplo, si especifica esta opción al mover un archivo a un directorio eliminará el directorio y reemplazarlo con el archivo.  
  
 Ciertos atributos de la **registro** objetos, como el [ParentURL](../../../ado/reference/ado-api/parenturl-property-ado.md) propiedad, no se actualizará una vez completada esta operación. Actualizar el **registro** propiedades del objeto al cerrar la **registro**, a continuación, vuelva a abrirlo con la dirección URL de la ubicación donde se ha movido el archivo o directorio.  
  
 Si este **registro** se obtuvo de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md), no se reflejará inmediatamente en la nueva ubicación del directorio o archivo movido el **Recordset**. Actualizar el **Recordset** al cerrar y volver a abrirlo.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Método Move (ADO)](../../../ado/reference/ado-api/move-method-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (ADO)](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)   
 [MoveFirst, MoveLast, MoveNext y MovePrevious métodos (RDS)](../../../ado/reference/rds-api/movefirst-movelast-movenext-and-moveprevious-methods-rds.md)
