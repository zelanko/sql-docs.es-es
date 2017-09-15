---
title: "Save (método) | Documentos de Microsoft"
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
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: edefe1c8d25abd84d5a5f82d7dde8035d82022ee
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="save-method"></a>Save (método)
Guarda el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) en un archivo o [flujo](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Destino*  
 Opcional. A **Variant** que representa el nombre de ruta de acceso completa del archivo donde el **Recordset** consiste en Guardar, o una referencia a un **flujo** objeto.  
  
 *PersistFormat*  
 Opcional. A [más](../../../ado/reference/ado-api/persistformatenum.md) valor que especifica el formato en el que el **Recordset** consiste en Guardar (XML o ADTG). El valor predeterminado es **adPersistADTG**.  
  
## <a name="remarks"></a>Comentarios  
 El [método Save](../../../ado/reference/ado-api/save-method.md) sólo se puede invocar el método en un formato de archivo **conjunto de registros**. Use la [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método de restauración más adelante el **Recordset** de *destino*.  
  
 Si el [propiedad Filter](../../../ado/reference/ado-api/filter-property.md) propiedad está en vigor para el **Recordset**, a continuación, se guardan únicamente las filas accesibles con el filtro. Si el **conjunto de registros** es jerárquico, a continuación, el elemento secundario actual **Recordset** y sus elementos secundarios se guardan, incluido el elemento primario **conjunto de registros**. Si el método Save de un elemento secundario **Recordset** es llama, el elemento secundario y todos sus elementos secundarios se guardan, pero el elemento primario no lo es.  
  
 La primera vez que guarde el **Recordset**, es opcional especificar *destino*. Si se omite *destino*, se creará un nuevo archivo con el nombre establecido en el valor de la propiedad de origen de la **conjunto de registros**.  
  
 Omitir *destino* cuando vuelve a llamar a **guardar** después de que se producirá la primera operación de guardar, o a un error de tiempo de ejecución. Si se llama posteriormente **guardar** con un nuevo *destino*, **Recordset** se guarda en el nuevo destino. Sin embargo, el nuevo destino y el destino original ambas estarán abiertos.  
  
 **Guardar** no cierra la **Recordset** o *destino*, por lo que puede seguir trabajando con el **Recordset** y guarde los cambios más recientes. *Destino* permanece abierta hasta que la **Recordset** está cerrado.  
  
 Por motivos de seguridad, el **guardar** método permite sólo el uso de la configuración de seguridad baja y personalizada de una secuencia de comandos ejecutada por Microsoft Internet Explorer.  
  
 Si el **guardar** método se llama durante una asincrónica **Recordset** capturar, ejecutar o actualizar la operación está en curso, a continuación, **guardar** espera a que la operación asincrónica está completa.  
  
 Los registros se guardan comenzando por la primera fila de la **conjunto de registros**. Cuando el **guardar** método termina, la posición actual de la fila se mueve a la primera fila de la **conjunto de registros**.  
  
 Para obtener los mejores resultados, establezca la [propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient** con **guardar**. Si el proveedor no admite todas las funciones necesarias para guardar **Recordset** objetos, el servicio de Cursor proporcionará esa funcionalidad.  
  
 Cuando un **Recordset** se mantiene con el **CursorLocation** propiedad establecida en **adUseServer**, la capacidad de actualización para el **Recordset**está limitado. Normalmente, solo las actualizaciones de tabla única, inserciones y eliminaciones se permiten (según la funcionalidad de proveedor). El [método Resync](../../../ado/reference/ado-api/resync-method.md) método también está disponible en esta configuración.  
  
> [!NOTE]
>  Guardar un **Recordset** con **campos** de tipo **adVariant**, **adIDispatch**, o **adIUnknown** es no compatible con ADO y puede provocar resultados imprevisibles.  
  
 Sólo los filtros con el formato de las cadenas de criterios (por ejemplo, OrderDate > ' 12/31/1999 ') afectan al contenido de un persistente **conjunto de registros**. Los filtros creados con una matriz de **marcadores** o mediante un valor de la [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) no se verá afectado el contenido de conservados **conjunto de registros**. Estas reglas se aplican a **Recordset**s creados con cursores de cliente o servidor.  
  
 Dado que la *destino* parámetro puede aceptar cualquier objeto que admita la interfaz IStream de OLE DB, puede guardar un **Recordset** directamente en el objeto Response de ASP. Para obtener más información, consulte el **escenario de persistencia de conjunto de registros XML**.  
  
 También puede guardar un **Recordset** en formato XML a una instancia de un objeto DOM de MSXML, como se muestra en el siguiente código de Visual Basic:  
  
```  
Dim xDOM As New MSXML.DOMDocument  
Dim rsXML As New ADODB.Recordset  
Dim sSQL As String, sConn As String  
  
sSQL = "SELECT customerid, companyname, contactname FROM customers"  
sConn="Provider=Microsoft.Jet.OLEDB.4.0;Data Source=Northwind.mdb"  
rsXML.Open sSQL, sConn  
rsXML.Save xDOM, adPersistXML   'Save Recordset directly into a DOM tree.  
...  
```  
  
> [!NOTE]
>  Existen dos limitaciones al guardar los conjuntos de registros jerárquicos (formas de datos) en formato XML. No se puede guardar en XML si el jerárquica **Recordset** contiene las actualizaciones pendientes, y no se puede guardar un con parámetros jerárquicos **conjunto de registros**.  
  
 A **Recordset** guardar en XML formato se guarda con formato UTF-8. Cuando se carga un archivo en un flujo de ADO, el objeto de secuencia no intentará abrir un **Recordset** de la secuencia, a menos que la propiedad juego de caracteres de la secuencia se establece en el valor adecuado para el formato UTF-8.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Guardar y abrir un ejemplo de los métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Guardar y abrir un ejemplo de los métodos (VC ++)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Open (método) (conjunto de registros ADO)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Open (método) (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)

