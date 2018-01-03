---
title: Objeto de conjunto de registros (ADO) | Documentos de Microsoft
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology: drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
f1_keywords: Recordset
helpviewer_keywords: Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: dec2c20c2450f4db1d0671f365714647c47c7db6
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="recordset-object-ado"></a>Objeto de conjunto de registros (ADO)
Representa todo el conjunto de registros de una tabla base o los resultados de un comando ejecutado. En cualquier momento, el **Recordset** objeto hace referencia a solo un único registro dentro del conjunto como el registro actual.  
  
## <a name="remarks"></a>Comentarios  
 Usa **Recordset** objetos para manipular los datos de un proveedor. Cuando se utiliza ADO, manipular datos casi por completo mediante **Recordset** objetos. Todos los **Recordset** objetos constan de registros (filas) y campos (columnas). Según la funcionalidad admitida por el proveedor, algunas **Recordset** métodos o propiedades no estén disponibles.  
  
 ADODB. Conjunto de registros es el ProgID que debe usarse para crear un **Recordset** objeto. Aplicaciones existentes que hacen referencia a la ADOR no actualizada. ProgID del conjunto de registros seguirá funcionando sin tener que recompilar, pero el nuevo desarrollo debe hacer referencia a ADODB. Conjunto de registros.  
  
 Hay cuatro tipos diferentes de cursor definidos en ADO:  
  
-   **Cursor dinámico** le permite ver las adiciones, cambios y eliminaciones realizadas por otros usuarios; permite que todos los tipos de movimiento a través de la **Recordset** que no se basa en marcadores; y permite marcadores si el proveedor admite ellos.  
  
-   **Cursores** se comporta como un cursor dinámico, salvo que TI no le permitirá ver los registros que otros usuarios agregar y evita el acceso a los registros que otros usuarios se eliminan. Cambios en los datos por otros usuarios seguirán estando visibles. Siempre admite marcadores y, por tanto, permite todos los tipos de movimiento a través de la **conjunto de registros**.  
  
-   **Cursor estático** proporciona una copia estática de un conjunto de registros que puede usar para buscar datos o generar informes; siempre admite marcadores y, por tanto, permite todos los tipos de movimiento a través de la **conjunto de registros**. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no serán visibles. Este es el único tipo de cursor permitido cuando se abre un cliente **Recordset** objeto.  
  
-   **Cursor de solo avance** permite sólo el desplazamiento hacia delante a través de la **conjunto de registros**. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no serán visibles. Esto mejora el rendimiento en situaciones donde es necesario hacer solo un único paso a través de un **conjunto de registros**.  
  
 Establecer el [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propiedad antes de abrir el **Recordset** para elegir el tipo de cursor o pasar un *CursorType* argumento con el [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)(método). Algunos proveedores no admiten todos los tipos de cursor. Consulte la documentación del proveedor. Si no se especifica un tipo de cursor, ADO abre un cursor de sólo avance de forma predeterminada.  
  
 Si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient** para abrir un **Recordset**, **UnderlyingValue** propiedad [Campo](../../../ado/reference/ado-api/field-object.md) objetos no está disponible en el valor devuelto **Recordset** objeto. Cuando se utiliza con algunos proveedores (por ejemplo, el proveedor ODBC de Microsoft para OLE DB junto con Microsoft SQL Server), puede crear **Recordset** objetos independientemente definida previamente [conexión](../../../ado/reference/ado-api/connection-object-ado.md)objeto pasando una cadena de conexión con el **abiertos** método. ADO sigue creando una [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto, pero no asignará ese objeto a una variable de objeto. Sin embargo, si se están abriendo varias **Recordset** objetos con la misma conexión, debe crear y abrir explícitamente un **conexión** objeto; esta asigna el **conexión**objeto a una variable de objeto. Si no utiliza esta variable de objeto al abrir el **Recordset** objetos, ADO creará un nuevo **conexión** objeto para cada nuevo **conjunto de registros**, incluso si se pasa el mismo cadena de conexión.  
  
 Puede crear tantos **Recordset** objetos según sea necesario.  
  
 Cuando se abre un **Recordset**, el registro actual se coloca en el primer registro (si existe) y la [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedades se establecen en **False**. Si no hay ningún registro, el **BOF** y **EOF** son valores de las propiedades **True**.  
  
 Puede usar el [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, y **MovePrevious** métodos; el [mover](../../../ado/reference/ado-api/move-method-ado.md) método; y el [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), y [filtro](../../../ado/reference/ado-api/filter-property.md) propiedades para volver a colocar el registro actual, suponiendo que el proveedor es compatible con la correspondiente funcionalidad. Solo avance **Recordset** objetos admiten solo el [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método. Cuando se usa el **mover** métodos para consultar cada registro (o enumerar el **Recordset**), puede usar el **BOF** y **EOF** propiedades para determinar si se ha movido más allá al principio o al final de la **conjunto de registros**.  
  
 Antes de usar cualquier funcionalidad de un **Recordset** objeto, debe llamar a la **admite** método del objeto que se va a comprobar que la funcionalidad es compatible o disponible. No debe utilizar la funcionalidad cuando la **admite** método devuelve false. Por ejemplo, puede usar el **MovePrevious** solo si de método `Recordset.Supports(adMovePrevious)` devuelve **True**. De lo contrario, obtendrá un error, porque la **Recordset** objetos que se han cerrado y deja de estar disponible en la instancia de la funcionalidad. Si no se admite una característica que le interesen, **admite** devolverá false también. En este caso, no debe llamar a la correspondiente propiedad o método en el **Recrodset** objeto.  
  
 **Conjunto de registros** objetos pueden admitir dos tipos de actualizaciones: inmediata y por lotes. En la actualización inmediata, todos los cambios a los datos se escriben de inmediato en el origen de datos subyacente una vez que se llama a la [actualización](../../../ado/reference/ado-api/update-method.md) método. También puede pasar matrices de valores como parámetros con el [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) y **actualizar** métodos y actualizar simultáneamente varios campos en un registro.  
  
 Si un proveedor admite la actualización por lotes, puede tener el proveedor de almacenar en caché los cambios en más de un registro y transmitirlos a continuación en una sola llamada a la base de datos con la [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Esto se aplica a los cambios realizados con el **AddNew**, **actualización**, y [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) métodos. Después de llamar a la **UpdateBatch** método, puede usar el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad para comprobar si los conflictos de datos con el fin de solucionarlos problemas asociados.  
  
> [!NOTE]
>  Para ejecutar una consulta sin utilizar un [comando](../../../ado/reference/ado-api/command-object-ado.md) de objetos, pasar una cadena de consulta para el **abiertos** método de un **Recordset** objeto. Sin embargo, un **comando** objeto es necesaria cuando desea conservar el texto del comando y volver a ejecutarlo o usar parámetros de consulta.  
  
 El [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad controla los permisos de acceso.  
  
 El **campos** colección es el miembro predeterminado de la **Recordset** objeto. Como resultado, las dos instrucciones de código siguientes son equivalentes.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Cuando un **Recordset** objeto se pasa a través de procesos, solo el **conjunto de filas** se calcular valores y las propiedades de la **conjunto de registros** se pasan por alto el objeto. Durante la unmarshalling, la **conjunto de filas** se desempaqueta en otra recién creada **Recordset** objeto, que también se establece sus propiedades en los valores predeterminados.  
  
 El **Recordset** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Eventos, métodos y propiedades del objeto de conjunto de registros](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Fields (colección) (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apéndice A: Proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
