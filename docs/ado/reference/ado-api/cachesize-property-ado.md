---
title: Propiedad CacheSize (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords:
- Recordset15::CacheSize
helpviewer_keywords:
- CacheSize property [ADO]
ms.assetid: 49dc9a49-af7b-433b-be36-7a14ca984fb7
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 29d5a36905a4de936dcac630adf97688d2b40855
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cachesize-property-ado"></a>Propiedad CacheSize (ADO)
Indica el número de registros de un [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) objetos que se almacenan en caché localmente en la memoria.  
  
## <a name="settings-and-return-values"></a>Configuración y valores devueltos  
 Establece o devuelve un **largo** valor que debe ser mayor que 0. Valor predeterminado es 1.  
  
## <a name="remarks"></a>Comentarios  
 Use la **CacheSize** propiedad para controlar cuántos registros para recuperar en una vez en la memoria local desde el proveedor. Por ejemplo, si la **CacheSize** es 10, tras abrir primero la **Recordset** de objeto, el proveedor recupera los 10 primeros registros en la memoria local. Conforme se desplaza por la **Recordset** de objeto, el proveedor devuelve los datos desde el búfer de memoria local. En cuanto mueva más allá del último registro en la memoria caché, el proveedor recupera los 10 siguientes registros del origen de datos en la memoria caché.  
  
> [!NOTE]
>  **CacheSize** se basa en el **máximo de filas abiertas** propiedades específicas del proveedor (en el **propiedades** colección de la **Recordset** objeto). No se puede establecer **CacheSize** en un valor mayor que **máximo de filas abiertas**. Para modificar el número de filas que se puede abrir el proveedor, establezca **máximo de filas abiertas**.  
  
 El valor de **CacheSize** se puede ajustar durante la vida de la **Recordset** objeto, pero si se cambia este valor solo afecta al número de registros en la memoria caché después de recuperaciones subsiguientes desde el origen de datos. Cambiar el valor de propiedad por sí sola no cambiará el contenido actual de la memoria caché.  
  
 Si hay muy pocos registros para recuperar que **CacheSize** especifica, el proveedor devuelve los registros restantes y se produce ningún error.  
  
 A **CacheSize** valor de cero no está autorizada y devuelve un error.  
  
 Registros recuperados de la memoria caché no reflejan cambios simultáneos realizados por otros usuarios al origen de datos. Para forzar una actualización de todos los datos almacenados en memoria caché, use la [Resync](../../../ado/reference/ado-api/resync-method.md) método.  
  
 Si **CacheSize** se establece en un valor mayor que uno, los métodos de navegación ([mover](../../../ado/reference/ado-api/move-method-ado.md), [MoveFirst, MoveLast, MoveNext y MovePrevious](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md)) puede dar lugar a la navegación a un eliminado el registro, si se produce una eliminación después de haber recuperaron los registros. Después de la operación de captura inicial, las eliminaciones posteriores no se reflejarán en la memoria caché de datos hasta que se intente tener acceso a un valor de datos de una fila eliminada. Sin embargo, establecer **CacheSize** a uno se elimina este problema ya que no se pueden recuperar filas eliminadas.  
  
## <a name="applies-to"></a>Se aplica a  
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)  
  
## <a name="see-also"></a>Vea también  
 [Ejemplo de la propiedad CacheSize (VB)](../../../ado/reference/ado-api/cachesize-property-example-vb.md)   
 [Ejemplo de la propiedad CacheSize (VC ++)](../../../ado/reference/ado-api/cachesize-property-example-vc.md)   
 [Ejemplo de la propiedad CacheSize (JScript)](../../../ado/reference/ado-api/cachesize-property-example-jscript.md)

