---
title: Método CopyRecord (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Record::raw_CopyRecord
- _Record::CopyRecord
helpviewer_keywords:
- CopyRecord method [ADO]
ms.assetid: b9bcf272-3c74-479f-95dd-0229a32e98fc
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: d11a8d5d775499246bd8af709764dec3f2ad61e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66698520"
---
# <a name="copyrecord-method-ado"></a>Método CopyRecord (ADO)
Copia una entidad representada por un [registro](../../../ado/reference/ado-api/record-object-ado.md) a otra ubicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
Record.CopyRecord (Source, Destination, UserName, Password, Options, Async)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Source*  
 Opcional. Un **cadena** valor que contiene la dirección URL que especifica la entidad que se va a copiar (por ejemplo, un archivo o directorio). Si *origen* se omite o se especifica una cadena vacía, el archivo o directorio representado por el actual [registro](../../../ado/reference/ado-api/record-object-ado.md) se va a copiar.  
  
 *Destino*  
 Opcional. Un **cadena** valor que contiene la dirección URL que especifica la ubicación donde *origen* se va a copiar.  
  
 *UserName*  
 Opcional. Un **cadena** valor que contiene el identificador de usuario que, si es necesario, autoriza el acceso a *destino*.  
  
 *Contraseña*  
 Opcional. Un **cadena** valor que contiene la contraseña que, si es necesario, comprueba *UserName*.  
  
 *Opciones*  
 Opcional. Un [CopyRecordOptionsEnum](../../../ado/reference/ado-api/copyrecordoptionsenum.md) valor que tiene un valor predeterminado de **como**. Especifica el comportamiento de este método.  
  
 *Async*  
 Opcional. Un **booleano** valor que, cuando **True**, especifica que esta operación debe ser asincrónica.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **cadena** valor que normalmente devuelve el valor de *destino*. Sin embargo, el valor devuelto exacto depende del proveedor.  
  
## <a name="remarks"></a>Comentarios  
 Los valores de *origen* y *destino* no debe ser idéntico; en caso contrario, se produce un error de tiempo de ejecución. Al menos uno de los nombres de servidor, la ruta de acceso o el recurso debe ser diferente.  
  
 Todos los elementos secundarios (por ejemplo, subdirectorios) de *origen* son copian de forma recursiva a menos que **adCopyNonRecursive** se especifica. En una operación recursiva, *destino* no debe ser un subdirectorio de *origen*; en caso contrario, no se completará la operación.  
  
 Este método produce un error si *destino* identifica una entidad existente (por ejemplo, un archivo o directorio), a menos que **adCopyOverWrite** se especifica.  
  
> [!IMPORTANT]
>  Use la **adCopyOverWrite** opción con prudencia. Por ejemplo, si especifica esta opción al copiar un archivo en un directorio le *eliminar* el directorio y reemplazarlo con el archivo.  
  
> [!NOTE]
>  Las direcciones URL con el esquema http, se invocarán automáticamente el [proveedor Microsoft OLE DB para la publicación en Internet](../../../ado/guide/appendixes/microsoft-ole-db-provider-for-internet-publishing.md). Para obtener más información, consulte [absoluto y las direcciones URL relativas](../../../ado/guide/data/absolute-and-relative-urls.md).  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
