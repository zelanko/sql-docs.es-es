---
title: La propiedad CacheSize (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 76cd9e4977ffda023c270a027602597ddf7b9a4a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724673"
---
# <a name="cachesize-property-ado"></a>Propiedad CacheSize (ADO)
Indica el número de registros desde un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objeto que se almacenan en caché localmente en memoria.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que debe ser mayor que 0. El valor predeterminado es 1.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CacheSize** propiedad para controlar el número de registros que para recuperar de una vez en la memoria local desde el proveedor. Por ejemplo, si la **CacheSize** es 10, después de abrir primero la **Recordset** objeto, el proveedor recupera los 10 primeros registros en la memoria local. Conforme se desplaza por la **Recordset** objeto, el proveedor devuelve los datos desde el búfer de memoria local. Tan pronto como se mueve más allá del último registro en la memoria caché, el proveedor recupera los 10 siguientes registros del origen de datos en la memoria caché.  
  
> [!NOTE]
>  **CacheSize** se basa en el **número máximo de filas abierto** propiedad específica del proveedor (en el **propiedades** colección de la **Recordset** objeto). No puede establecer **CacheSize** en un valor mayor que **número máximo de filas abierto**. Para modificar el número de filas que se puede abrir el proveedor, establezca **número máximo de filas abierto**.  
  
 El valor de **CacheSize** se puede ajustar durante la vigencia de la **Recordset** objeto, pero al cambiar este valor solo afecta al número de registros en la memoria caché después de recuperaciones posteriores desde el origen de datos. Cambiar el valor de propiedad por sí solo no cambiará el contenido actual de la memoria caché.  
  
 Si hay menos registros que se recuperan de **CacheSize** especifica, el proveedor devuelve los registros restantes y se produce ningún error.  
  
 Un **CacheSize** valor de cero no se permite y devuelve un error.  
  
 Registros recuperados de la memoria caché no reflejan los cambios simultáneos realizados por otros usuarios a los datos de origen. Para forzar una actualización de todos los datos almacenados en caché, use el [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Si **CacheSize** se establece en un valor mayor que uno, los métodos de navegación ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) puede dar lugar a la navegación a un Eliminar registro, si se produce una eliminación después de haber recuperaron los registros. Después de la operación de captura inicial, las eliminaciones posteriores no se reflejarán en la caché de datos hasta que intente obtener acceso a un valor de datos de una fila eliminada. Sin embargo, establecer **CacheSize** a uno se elimina este problema ya que no se pueden capturar las filas eliminadas.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad CacheSize (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [Ejemplo de la propiedad CacheSize (VC ++)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [Ejemplo de la propiedad CacheSize (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)
