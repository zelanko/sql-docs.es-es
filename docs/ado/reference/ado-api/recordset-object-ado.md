---
title: Objeto de conjunto de registros (ADO) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- Recordset
helpviewer_keywords:
- Recordset object [ADO]
ms.assetid: ede1415f-c3df-4cc5-a05b-2576b2b84b60
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: cc95d6ef7e61dcde373a646359d134dce0b3389d
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/05/2019
ms.locfileid: "66711943"
---
# <a name="recordset-object-ado"></a>Objeto de conjunto de registros (ADO)
Representa todo el conjunto de registros de una tabla base o los resultados de un comando ejecutado. En cualquier momento, el **Recordset** objeto hace referencia a solo un único registro dentro del conjunto como el registro actual.  
  
## <a name="remarks"></a>Comentarios  
 Usa **Recordset** objetos para manipular los datos de un proveedor. Cuando se utiliza ADO, manipular datos casi por completo mediante **Recordset** objetos. Todos los **Recordset** objetos constan de registros (filas) y campos (columnas). Según la funcionalidad admitida por el proveedor, algunos **Recordset** métodos o propiedades no estén disponibles.  
  
 ADODB. Conjunto de registros es el identificador de programa que debe usarse para crear un **Recordset** objeto. Aplicaciones existentes que hacen referencia a objeto ADOR obsoleta. ProgID del objeto Recordset seguirán funcionando sin volver a compilar, pero debe hacer referencia a ADODB nuevo desarrollo. Conjunto de registros.  
  
 Hay cuatro tipos diferentes de cursor definidos en ADO:  
  
-   **Cursor dinámico** le permite ver las adiciones, cambios y eliminaciones realizadas por otros usuarios; permite que todos los tipos de movimiento a través de la **Recordset** que no se basa en marcadores; y permite marcadores si el proveedor admite ellos.  
  
-   **Cursores KEYSET** Behaves como un cursor dinámico, salvo que TI impide que vea los registros que otros usuarios agregar y evita el acceso a los registros que otros usuarios a eliminar. Cambios en los datos por otros usuarios seguirán estando visibles. Siempre admite marcadores y, por tanto, permite todos los tipos de movimiento a través de la **Recordset**.  
  
-   **Cursor estático** proporciona una copia estática de un conjunto de registros que puede usar para buscar datos o generar informes; siempre admite marcadores y, por tanto, permite todos los tipos de movimiento a través de la **Recordset**. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no será visibles. Este es el único tipo de cursor permitido cuando se abre un cliente **Recordset** objeto.  
  
-   **Cursor de solo avance** permite sólo hacia delante a través de la **Recordset**. Las adiciones, cambios o eliminaciones realizadas por otros usuarios no será visibles. Esto mejora el rendimiento en situaciones donde es necesario hacer sólo un único paso a través de un **Recordset**.  
  
 Establecer el [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propiedad antes de abrir el **Recordset** para elegir el tipo de cursor o pasar un *CursorType* argumento con el [abrir](../../../ado/reference/ado-api/open-method-ado-recordset.md)método. Algunos proveedores no admiten todos los tipos de cursor. Compruebe la documentación del proveedor. Si no especifica un tipo de cursor, ADO abre un cursor de solo avance de forma predeterminada.  
  
 Si el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad está establecida en **adUseClient** para abrir un **Recordset**, **UnderlyingValue** propiedad [Campo](../../../ado/reference/ado-api/field-object.md) objetos no está disponible en el valor devuelto **Recordset** objeto. Cuando se usa con algunos proveedores (por ejemplo, el proveedor ODBC de Microsoft para OLE DB junto con Microsoft SQL Server), puede crear **Recordset** objetos independientemente definidos previamente [conexión](../../../ado/reference/ado-api/connection-object-ado.md)pasando una cadena de conexión con el **abierto** método. ADO sigue creando un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) objeto, pero no asignará ese objeto a una variable de objeto. Sin embargo, si va a abrir varios **Recordset** objetos a través de la misma conexión, debe crear y abrir explícitamente un **conexión** objeto; este asigna el **conexión**objeto a una variable de objeto. Si no se use esta variable de objeto al abrir su **Recordset** objetos, crea un nuevo ADO **conexión** objeto para cada nuevo **Recordset**, incluso si pasa el mismo cadena de conexión.  
  
 Puede crear tantos **Recordset** objetos según sea necesario.  
  
 Al abrir un **Recordset**, el registro actual se coloca en el primer registro (si existe) y el [BOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) y [EOF](../../../ado/reference/ado-api/bof-eof-properties-ado.md) propiedades se establecen en **False**. Si no hay ningún registro, el **BOF** y **EOF** son valores de propiedad **True**.  
  
 Puede usar el [MoveFirst](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md), **MoveLast**, **MoveNext**, y **MovePrevious** métodos; el [mover](../../../ado/reference/ado-api/move-method-ado.md) método; y el [AbsolutePosition](../../../ado/reference/ado-api/absoluteposition-property-ado.md), [AbsolutePage](../../../ado/reference/ado-api/absolutepage-property-ado.md), y [filtro](../../../ado/reference/ado-api/filter-property.md) propiedades para volver a colocar el registro actual, suponiendo que el proveedor es compatible con la correspondiente funcionalidad. Solo avance **Recordset** objetos admiten solo el [MoveNext](../../../ado/reference/ado-api/movefirst-movelast-movenext-and-moveprevious-methods-ado.md) método. Cuando se usa el **mover** métodos para visitar cada registro (o enumerar el **Recordset**), puede usar el **BOF** y **EOF** propiedades para determinar si se ha movido más allá del principio o al final de la **Recordset**.  
  
 Antes de usar cualquier funcionalidad de un **Recordset** objeto, debe llamar a la **admite** método en el objeto para comprobar que la funcionalidad se admite ni está disponible. No debe utilizar la funcionalidad cuando la **admite** método devuelve false. Por ejemplo, puede usar el **MovePrevious** método sólo si `Recordset.Supports(adMovePrevious)` devuelve **True**. De lo contrario, obtendrá un error, porque el **Recordset** objeto se han cerrado y la funcionalidad representa no está disponible en la instancia. Si no se admite una característica que le interese, **admite** devolverá false también. En este caso, debe evitar llamar a la correspondiente propiedad o método en el **Recordset** objeto.  
  
 **Conjunto de registros** objetos pueden admitir dos tipos de actualizaciones: inmediata y por lotes. En la actualización inmediata, todos los cambios a los datos se escriben inmediatamente en el origen de datos subyacente una vez que se llama a la [actualización](../../../ado/reference/ado-api/update-method.md) método. También puede pasar matrices de valores como parámetros con el [AddNew](../../../ado/reference/ado-api/addnew-method-ado.md) y **actualizar** métodos y actualizar simultáneamente varios campos de un registro.  
  
 Si un proveedor admite la actualización por lotes, puede hacer que el proveedor de almacenar en caché los cambios en más de un registro y, a continuación, transmitirlos en una sola llamada a la base de datos con el [UpdateBatch](../../../ado/reference/ado-api/updatebatch-method.md) método. Esto se aplica a los cambios realizados con los **AddNew**, **actualización**, y [eliminar](../../../ado/reference/ado-api/delete-method-ado-recordset.md) métodos. Después de llamar a la **UpdateBatch** método, puede usar el [estado](../../../ado/reference/ado-api/status-property-ado-recordset.md) propiedad que se va a comprobar los conflictos de datos para resolverlos.  
  
> [!NOTE]
>  Para ejecutar una consulta sin utilizar un [comando](../../../ado/reference/ado-api/command-object-ado.md) de objeto, pase una cadena de consulta a la **abierto** método de un **Recordset** objeto. Sin embargo, un **comando** se requiere el objeto cuando desea conservar el texto del comando y vuelva a ejecutarla o usar parámetros de consulta.  
  
 El [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad rige los permisos de acceso.  
  
 El **campos** colección es el miembro predeterminado de la **Recordset** objeto. Como resultado, las dos instrucciones de código siguientes son equivalentes.  
  
```  
Debug.Print objRs.Fields.Item(0)  ' Both statements print   
Debug.Print objRs(0)              '  the Value of Item(0).  
```  
  
 Cuando un **Recordset** objeto se pasa a través de procesos, solo el **conjunto de filas** valores están en el búfer y las propiedades de la **Recordset** objeto se omiten. Durante la unmarshalling, el **conjunto de filas** se desempaqueta en otra recién creada **Recordset** objeto, lo que también establece sus propiedades en los valores predeterminados.  
  
 El **Recordset** objeto es seguro para scripting.  
  
 Esta sección contiene el siguiente tema.  
  
-   [Los eventos, métodos y propiedades del objeto de conjunto de registros](../../../ado/reference/ado-api/recordset-object-properties-methods-and-events.md)  
  
## <a name="see-also"></a>Vea también  
 [Objeto de conexión (ADO)](../../../ado/reference/ado-api/connection-object-ado.md)   
 [Colección de campos (ADO)](../../../ado/reference/ado-api/fields-collection-ado.md)   
 [Colección de propiedades (ADO)](../../../ado/reference/ado-api/properties-collection-ado.md)   
 [Apéndice A: proveedores](../../../ado/guide/appendixes/appendix-a-providers.md)
