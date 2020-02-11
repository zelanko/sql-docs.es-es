---
title: Traslado de una base de datos Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- moving databases [Anlysis Services]
- moving databases
- operations [Analysis Services - multidimensional data]
ms.assetid: fa644e5d-e276-445e-98d9-673afcfb83fe
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 02d084aea4491982d560f1cf0b8dc449b8502f09
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073598"
---
# <a name="move-an-analysis-services-database"></a>Mover una base de datos de Analysis Services
  Con frecuencia, se producen situaciones en las que un administrador de base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quiere mover una base de datos modelo multidimensional o tabular a otra ubicación. Estas situaciones suelen responder a necesidades empresariales, como mover la base de datos a otro disco para mejorar el rendimiento, disponer de más espacio para que la base de datos pueda crecer o actualizar un producto.  
  
 Una base de datos se puede mover de muchas maneras. En este documento se describen los siguientes escenarios comunes:  
  
-   Usar SSMS de forma interactiva  
  
-   Usar programación a través de AMO  
  
-   Usar script XMLA  
  
 En todos los escenarios se requiere que el usuario tenga acceso a la carpeta de la base de datos y que use un método para mover los archivos al destino final deseado.  
  
> [!NOTE]  
>  Si se separa una base de datos sin asignarla antes una contraseña, quedará desprotegida. Se recomienda asignar una contraseña a la base de datos para proteger la información confidencial. Además, se deberá aplicar la seguridad de acceso correspondiente a la carpeta, las subcarpetas y los archivos de la base de datos para impedir el acceso no autorizado.  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="moving-a-database-interactively-using-ssms"></a>Mover una base de datos interactivamente mediante SSMS  
  
1.  Localice la base de datos que desea mover en el panel izquierdo o derecho de SSMS.  
  
2.  Haga clic con el botón derecho en la base de datos y seleccione **desasociar..** .  
  
3.  Asigne una contraseña a la base de datos que se va separar y, a continuación, haga clic en **Aceptar** para ejecutar el comando Detach.  
  
4.  Use cualquier mecanismo del sistema operativo o el método que emplee normalmente para mover archivos con objeto de mover la carpeta de la base de datos a la nueva ubicación.  
  
5.  Localice la carpeta **Bases de datos** en el panel izquierdo o derecho de SSMS.  
  
6.  Haga clic con el botón derecho en la carpeta **bases** de **datos y seleccione adjuntar..** .  
  
7.  En el cuadro de texto **Carpeta** , escriba la nueva ubicación de la carpeta de la base de datos. Como alternativa, puede usar el botón Examinar (**...**) para buscar la carpeta de la base de datos.  
  
8.  Seleccione el `ReadWrite` modo de la base de datos.  
  
9. Escriba la contraseña que se usó en el paso 3 y haga clic en **Aceptar** para ejecutar el comando Attach.  
  
#### <a name="moving-a-database-programmatically-using-amo"></a>Mover una base de datos mediante programación a través de AMO  
  
1.  En la aplicación C#, adapte el código de ejemplo siguiente y complete las tareas indicadas.  
  
 `private void MoveDb(Server server, string dbName,`  
  
 `string dbInitialLocation, string dbFinalLocation,`  
  
 `string dbPassword, ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `//Verify dbInitialLocation exists before continuing`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `//Save current cursor and change cursor to Cursors.WaitCursor`  
  
 `db = server.Databases[dbName];`  
  
 `db.Detach(dbPassword);`  
  
 `//Add your own code to copy the database files to the destination where you intend to attach the database`  
  
 `//Verify dbFinalLocation exists before continuing`  
  
 `server.Attach(dbFinalLocation, dbReadWriteMode, dbPassword);`  
  
 `//Restore cursor to its original`  
  
 `}`  
  
 `}`  
  
1.  En la aplicación C#, invoque `MoveDb()` con los parámetros necesarios.  
  
2.  Compile y ejecute el código para mover la base de datos.  
  
#### <a name="moving-a-database-by-script-using-xmla"></a>Mover una base de datos mediante script XMLA  
  
1.  Abra una nueva pestaña XMLA en SSMS.  
  
2.  Copie la plantilla de script siguiente para XMLA  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Reemplace `%dbName%` por el nombre de la base de datos y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
3.  Use cualquier mecanismo del sistema operativo o el método que emplee normalmente para mover archivos con objeto de mover la carpeta de la base de datos a la nueva ubicación.  
  
4.  Copie la plantilla de script siguiente para XMLA en una nueva pestaña XMLA  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Reemplace `%dbFolder%` por la ruta UNC completa de la carpeta de la base de datos, `%ReadOnlyMode%` por el valor `ReadOnly` o `ReadWrite` correspondiente, y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Ubicación de almacenamiento de base de datos](database-storage-location.md)   
 [Base de datos Readwritemode](database-readwritemodes.md)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
