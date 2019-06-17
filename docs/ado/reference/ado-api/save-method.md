---
title: Save (método) | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
f1_keywords:
- _Recordset::Save
- _Recordset::raw_Save
helpviewer_keywords:
- Save method [ADO]
ms.assetid: ed3d9678-5c28-4e61-8bb3-7dfb66d99cf5
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 0953b76ff642387679c907e6f0b3364cbac898df
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66711386"
---
# <a name="save-method"></a>Save (método)
Guarda el [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) en un archivo o [Stream](../../../ado/reference/ado-api/stream-object-ado.md) objeto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
recordset.Save Destination, PersistFormat  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Destino*  
 Opcional. Un **Variant** que representa el nombre de ruta de acceso completa del archivo donde el **Recordset** en guardarse, o una referencia a un **Stream** objeto.  
  
 *PersistFormat*  
 Opcional. Un [más](../../../ado/reference/ado-api/persistformatenum.md) valor que especifica el formato en el que el **Recordset** en guardarse (XML o ADTG). El valor predeterminado es **adPersistADTG**.  
  
## <a name="remarks"></a>Comentarios  
 El [método Save](../../../ado/reference/ado-api/save-method.md) sólo se puede invocar el método en una página abierta **Recordset**. Use la [método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md) método restaurar más adelante el **Recordset** desde *destino*.  
  
 Si el [propiedad Filter](../../../ado/reference/ado-api/filter-property.md) propiedad está en vigor para la **Recordset**, a continuación, se guardan las filas accesibles con el filtro. Si el **Recordset** es jerárquico, a continuación, el elemento secundario actual **Recordset** y sus elementos secundarios se guardan, incluido el elemento primario **Recordset**. Si el método Save de un elemento secundario **Recordset** es llama, el elemento secundario y todos sus elementos secundarios se guardan, pero el elemento primario no lo es.  
  
 La primera vez que guarde el **Recordset**, es opcional especificar *destino*. Si se omite *destino*, se creará un nuevo archivo con un nombre establecido en el valor de la propiedad de origen de la **Recordset**.  
  
 Omitir *destino* cuando se llama posteriormente **guardar** después de que se producirá la primera operación de guardar, o un error en tiempo de ejecución. Si se llama posteriormente **guardar** con un nuevo *destino*, **Recordset** se guarda en el nuevo destino. Sin embargo, el nuevo destino y el destino original ambos será abiertos.  
  
 **Guardar** no cierra la **Recordset** o *destino*, por lo que puede seguir trabajando con el **Recordset** y guarde los cambios más recientes. *Destino* permanece abierta hasta que el **Recordset** está cerrado.  
  
 Por motivos de seguridad, el **guardar** método permite solo el uso de la configuración de seguridad baja y personalizada de un script ejecutado por Microsoft Internet Explorer.  
  
 Si el **guardar** se llama al método asincrónico mientras se **Recordset** capturar, ejecutar o actualizar la operación está en curso, a continuación, **guardar** espera a que la operación asincrónica completada.  
  
 Se guardan los registros a partir de la primera fila de la **Recordset**. Cuando el **guardar** método finaliza, la posición actual de la fila se mueve a la primera fila de la **Recordset**.  
  
 Para obtener mejores resultados, establezca el [propiedad CursorLocation (ADO)](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient** con **guardar**. Si el proveedor no admite todas las funciones necesarias para guardar **Recordset** objetos, el servicio de cursores proporcionará esa funcionalidad.  
  
 Cuando un **Recordset** se mantiene con la **CursorLocation** propiedad establecida en **adUseServer**, la capacidad de actualización para el **Recordset**está limitado. Normalmente, solo las actualizaciones de tabla única, las inserciones y eliminaciones se permiten (según la funcionalidad de proveedor). El [método Resync](../../../ado/reference/ado-api/resync-method.md) método también está disponible en esta configuración.  
  
> [!NOTE]
>  Guardar un **Recordset** con **campos** typu **adVariant**, **adIDispatch**, o **adChapter** es no compatible con ADO y puede causar resultados imprevisibles.  
  
 Solo se filtra en forma de cadenas de criterios (p. ej., OrderDate > ' 12/31/1999 ') afectan al contenido de un persistente **Recordset**. Los filtros creados con una matriz de **marcadores** o mediante un valor de la [FilterGroupEnum](../../../ado/reference/ado-api/filtergroupenum.md) no afectarán al contenido de conservados **Recordset**. Estas reglas se aplican a **Recordset**s se creó con los cursores del lado cliente o servidor.  
  
 Dado que el *destino* parámetro puede aceptar cualquier objeto que admita la interfaz IStream de OLE DB, puede guardar un **Recordset** directamente en el objeto de respuesta de ASP. Para obtener más información, consulte el **escenario de persistencia de conjunto de registros XML**.  
  
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
>  Existen dos limitaciones al guardar los conjuntos de registros jerárquicos (formas de datos) en formato XML. No se puede guardar en XML si el jerárquica **Recordset** contiene las actualizaciones pendientes, y no se puede guardar un con parámetros jerárquicos **Recordset**.  
  
 Un **Recordset** guarda XML en el formato se guarda con formato UTF-8. Cuando este archivo se carga en un Stream de ADO, el objeto Stream no intentará abrir un **Recordset** de la secuencia, a menos que la propiedad juego de caracteres de la secuencia se establece en el valor adecuado para el formato UTF-8.  
  
## <a name="applies-to"></a>Se aplica a  
  
|||  
|-|-|  
|[Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)|[Objeto de secuencia (ADO)](../../../ado/reference/ado-api/stream-object-ado.md)|  
  
## <a name="see-also"></a>Vea también  
 [Guardar y abrir un ejemplo de los métodos (VB)](../../../ado/reference/ado-api/save-and-open-methods-example-vb.md)   
 [Guardar y abrir un ejemplo de los métodos (VC ++)](../../../ado/reference/ado-api/save-and-open-methods-example-vc.md)   
 [Método Open (ADO Recordset)](../../../ado/reference/ado-api/open-method-ado-recordset.md)   
 [Método Open (Stream de ADO)](../../../ado/reference/ado-api/open-method-ado-stream.md)   
 [Método SaveToFile](../../../ado/reference/ado-api/savetofile-method.md)
