---
title: Almacenamiento de datos | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b89f05822ee23f5ad62c627b8bc6d67ebe401a2e
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52527633"
---
# <a name="persisting-data"></a>Conservar los datos
Equipos portátiles (por ejemplo, con equipos portátiles) ha generado la necesidad de las aplicaciones que se pueden ejecutar en un estado conectado y desconectado. ADO ha agregado compatibilidad para esto proporcionando al programador la capacidad de guardar un cursor de cliente **Recordset** en el disco y vuelva a cargar más adelante.  
  
 Hay varios escenarios en los que podría usar este tipo de característica, incluidos los siguientes:  
  
-   **Viaje:** Al tomar la aplicación en la carretera, es fundamental para proporcionar la capacidad de realizar cambios y agregar nuevos registros que, a continuación, se vuelve a conectar a la base de datos más adelante y confirmados.  
  
-   **Búsquedas se actualizan con frecuencia:** A menudo en una aplicación, se usan tablas como búsquedas-por ejemplo, tablas de impuestos de estado. Se actualizan con poca frecuencia y son de solo lectura. En lugar de volver a leer estos datos desde el servidor cada vez que se inicia la aplicación, simplemente la aplicación puede cargar los datos desde persistente localmente **Recordset**.  
  
 En ADO, para guardar y cargar **conjuntos de registros**, utilice el **Recordset.Save** y **Recordset.Open(,,,adCmdFile)** métodos en ADO **Recordset**objeto.  
  
 Puede usar el **Guardar conjunto de registros** método para conservar su ADO **Recordset** a un archivo en un disco. (También puede guardar un **Recordset** a ADO **Stream** objeto. **Stream** objetos se describen más adelante en la guía.) Más adelante, puede utilizar el **abierto** método para volver a abrir el **Recordset** cuando esté listo para usarlo. De forma predeterminada, ADO guarda el **Recordset** en el formato registrado de Microsoft Advanced Data TableGram (ADTG). Este formato binario se especifica mediante el **adPersistADTG más** valor. Como alternativa, puede elegir guardar su **Recordset** fuera como XML en lugar de utilizar **adPersistXML**. Para obtener más información acerca de cómo guardar los conjuntos de registros como XML, vea [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 La sintaxis de la **guardar** método es como sigue:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 La primera vez que guarde el **Recordset**, es opcional especificar *destino*. Si se omite *destino*, se creará un nuevo archivo con un nombre establecido en el valor de la [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad de la **Recordset**.  
  
 Omitir *destino* cuando se llama posteriormente **guardar** después de que se producirá un error en tiempo de ejecución o la primera operación de guardar. Si se llama posteriormente **guardar** con un nuevo *destino*, **Recordset** se guarda en el nuevo destino. Sin embargo, el nuevo destino y el destino original ambos será abiertos.  
  
 **Guardar** no cierra la **Recordset** o *destino*, por lo que puede seguir trabajando con el **Recordset** y guarde los cambios más recientes. *Destino* permanece abierta hasta que el **Recordset** está cerrada, durante el cual pueden leer pero no escribir en otras aplicaciones *destino*.  
  
 Por motivos de seguridad, el **guardar** método permite solo el uso de la configuración de seguridad baja y personalizada de un script ejecutado por Microsoft Internet Explorer.  
  
 Si el **guardar** se llama al método asincrónico mientras se **Recordset** capturar, ejecutar o actualizar la operación está en curso, **guardar** espera hasta que la operación asincrónica completar.  
  
 Se guardan los registros a partir de la primera fila de la **Recordset**. Cuando el **guardar** método finaliza, la posición actual de la fila se mueve a la primera fila de la **Recordset**.  
  
 Para obtener mejores resultados, establezca el [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient** con **guardar**. Si el proveedor no admite todas las funciones necesarias para guardar **Recordset** objetos, el servicio de cursores proporcionará esa funcionalidad.  
  
 Cuando un **Recordset** se mantiene con la **CursorLocation** propiedad establecida en **adUseServer**, la capacidad de actualización para el **Recordset**está limitado. Normalmente, solo las actualizaciones de tabla única, las inserciones y eliminaciones se permiten (según la funcionalidad de proveedor). El [Resync](../../../ado/reference/ado-api/resync-method.md) método también está disponible en esta configuración.  
  
 Dado que el *destino* parámetro puede aceptar cualquier objeto que es compatible con OLE DB **IStream** interfaz, puede guardar un **Recordset** directamente a ASP  **Respuesta** objeto.  
  
 En el ejemplo siguiente, la **guardar** y **abierto** métodos se usan para conservar un **Recordset** y abrirlo posteriormente:  
  
```  
'BeginPersist  
   conn.ConnectionString = _  
   "Provider=SQLOLEDB;Data Source=MySQLServer;" _  
      & "Integrated Security=SSPI;Initial Catalog=pubs"  
   conn.Open  
  
   conn.Execute "create table testtable (dbkey int " & _  
      "primary key, field1 char(10))"  
   conn.Execute "insert into testtable values (1, 'string1')"  
  
   Set rst.ActiveConnection = conn  
   rst.CursorLocation = adUseClient  
  
   rst.Open "select * from testtable", conn, adOpenStatic, _  
      adLockBatchOptimistic  
  
   'Change the row on the client  
   rst!field1 = "NewValue"  
  
   'Save to a file--the .dat extension is an example; choose  
   'your own extension. The changes will be saved in the file  
   'as well as the original data.  
   MyFile = Dir("c:\temp\temptbl.dat")  
   If MyFile <> "" Then  
       Kill "c:\temp\temptbl.dat"  
   End If  
  
   rst.Save "c:\temp\temptbl.dat", adPersistADTG  
   Set rst = Nothing  
  
   'Now reload the data from the file  
   Set rst = New ADODB.Recordset  
   rst.Open "c:\temp\temptbl.dat", , adOpenStatic, _  
      adLockBatchOptimistic, adCmdFile  
  
   Debug.Print "After Loading the file from disk"  
   Debug.Print "   Current Edited Value: " & rst!field1.Value  
   Debug.Print "   Value Before Editing: " & rst!field1.OriginalValue  
  
   'Note that you can reconnect to a connection and  
   'submit the changes to the data source  
   Set rst.ActiveConnection = conn  
   rst.UpdateBatch  
'EndPersist  
```  
  
## <a name="remarks"></a>Comentarios  
 Esta sección contiene los temas siguientes.  
  
-   [Más información acerca de la persistencia de conjunto de registros](../../../ado/guide/data/more-about-recordset-persistence.md)  
  
-   [Almacenar conjuntos de registros filtrados y jerárquicos](../../../ado/guide/data/persisting-filtered-and-hierarchical-recordsets.md)  
  
-   [Almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md)
