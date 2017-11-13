---
title: Conservar los datos | Documentos de Microsoft
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- persisting data [ADO]
- data updates [ADO], persisting data
- data persistence [ADO]
- updating data [ADO], persisting data
ms.assetid: 21c162ca-2845-4dd8-a49d-e715aba8c461
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f9862fc9f45674d3995b857eec222d8f560870a6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="persisting-data"></a>Conservar los datos
Equipos portátiles (por ejemplo, con equipos portátiles) ha generado la necesidad de aplicaciones que se ejecutan en un estado conectado y desconectado. ADO ha agregado compatibilidad para esta funcionalidad ofreciendo al programador la capacidad de guardar un cursor de cliente **Recordset** en el disco y cargarlo de nuevo más tarde.  
  
 Hay varios escenarios en los que podría utilizar este tipo de característica, incluidos los siguientes:  
  
-   **Viaje:** al llevar a cabo la aplicación en la carretera, es fundamental para proporcionar la capacidad de realizar cambios y agregar nuevos registros que pueden, a continuación, se vuelve a conectar a la base de datos más adelante y se confirman.  
  
-   **Actualizan con poca frecuencia de búsquedas:** a menudo en una aplicación, se usan tablas como búsquedas, por ejemplo, tablas de impuestos de estado. Se actualizan con poca frecuencia y son de solo lectura. En lugar de volver a leer estos datos desde el servidor cada vez que se inicia la aplicación, simplemente la aplicación puede cargar los datos de persistente localmente **conjunto de registros**.  
  
 En ADO, para guardar y cargar **conjuntos de registros**, use la **Recordset.Save** y **Recordset.Open(,,,adCmdFile)** métodos en la propiedad ADO **Recordset**objeto.  
  
 Puede usar el **guardar de conjunto de registros** método para conservar su ADO **Recordset** a un archivo en un disco. (También puede guardar un **Recordset** a ADO **flujo** objeto. **Transmitir** objetos se describen más adelante en la guía.) Posteriormente, puede utilizar el **abiertos** método para volver a abrir la **Recordset** cuando esté listo para usarlo. De forma predeterminada, ADO guarda el **Recordset** en el formato propietario Advanced Data TableGram (ADTG) de Microsoft. Este formato binario se especifica mediante la **adPersistADTG más** valor. Como alternativa, puede elegir guardar la **Recordset** fuera como XML en lugar de utilizar **adPersistXML**. Para obtener más información acerca de cómo guardar conjuntos de registros como XML, vea [almacenar registros en formato XML](../../../ado/guide/data/persisting-records-in-xml-format.md).  
  
 La sintaxis de la **guardar** método es como sigue:  
  
```  
  
recordset.  
Save  
Destination, PersistFormat  
  
```  
  
 La primera vez que guarde el **Recordset**, es opcional especificar *destino*. Si se omite *destino*, se creará un nuevo archivo con el nombre establecido en el valor de la [origen](../../../ado/reference/ado-api/source-property-ado-recordset.md) propiedad de la **conjunto de registros**.  
  
 Omitir *destino* cuando vuelve a llamar a **guardar** después de que se producirá un error en tiempo de ejecución o la primera operación de guardar. Si se llama posteriormente **guardar** con un nuevo *destino*, **Recordset** se guarda en el nuevo destino. Sin embargo, el nuevo destino y el destino original ambas estarán abiertos.  
  
 **Guardar** no cierra la **Recordset** o *destino*, por lo que puede seguir trabajando con el **Recordset** y guarde los cambios más recientes. *Destino* permanece abierta hasta que la **Recordset** está cerrada, durante el cual pueden leer pero no escribir en otras aplicaciones *destino*.  
  
 Por motivos de seguridad, el **guardar** método permite sólo el uso de la configuración de seguridad baja y personalizada de una secuencia de comandos ejecutada por Microsoft Internet Explorer.  
  
 Si el **guardar** método se llama durante una asincrónica **Recordset** capturar, ejecutar o actualizar la operación está en curso, **guardar** espera hasta que la operación asincrónica completar.  
  
 Los registros se guardan comenzando por la primera fila de la **conjunto de registros**. Cuando el **guardar** método termina, la posición actual de la fila se mueve a la primera fila de la **conjunto de registros**.  
  
 Para obtener los mejores resultados, establezca la [CursorLocation](../../../ado/reference/ado-api/cursorlocation-property-ado.md) propiedad **adUseClient** con **guardar**. Si el proveedor no admite todas las funciones necesarias para guardar **Recordset** objetos, el servicio de Cursor proporcionará esa funcionalidad.  
  
 Cuando un **Recordset** se mantiene con el **CursorLocation** propiedad establecida en **adUseServer**, la capacidad de actualización para el **Recordset**está limitado. Normalmente, solo las actualizaciones de tabla única, inserciones y eliminaciones se permiten (depende de la funcionalidad de proveedor). El [Resync](../../../ado/reference/ado-api/resync-method.md) método también está disponible en esta configuración.  
  
 Dado que la *destino* parámetro puede aceptar cualquier objeto que admita OLE DB **IStream** interfaz, puede guardar un **conjunto de registros** directamente a la ASP  **Respuesta** objeto.  
  
 En el ejemplo siguiente, la **guardar** y **abiertos** métodos se usan para conservar un **Recordset** y abrirlo posteriormente:  
  
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

