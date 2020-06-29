---
title: Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
author: minewiskan
ms.author: owend
ms.openlocfilehash: 2a1496bee303e94720a354002e63cefcf479df85
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468920"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services
  Con frecuencia se producen situaciones en las que un administrador de bases de datos (dba) de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] quiere cambiar el modo de lectura/escritura de una base de datos tabular o multidimensional. Estas situaciones suelen responder a necesidades empresariales, como compartir la base de datos entre un grupo de servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para proporcionar una mejor experiencia para el usuario.  
  
 El modo de una base de datos se puede cambiar de muchas formas. En este documento se describen los siguientes escenarios comunes:  
  
-   Usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usar programación a través de AMO  
  
-   Usar script XMLA  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Para cambiar el modo de lectura/escritura de una base de datos de forma interactiva mediante Management Studio  
  
1.  Localice la base de datos en el panel izquierdo o derecho de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Haga clic con el botón secundario en la base de datos y seleccione **propiedades**. Busque la carpeta de la base de datos y anote su ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
    > [!IMPORTANT]  
    >  En cuanto se separa la base de datos, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ya no puede ayudarle a obtener su ubicación.  
  
3.  Haga clic con el botón derecho en la base de datos y seleccione **desasociar..** .  
  
4.  Asigne una contraseña a la base de datos que se va separar y, a continuación, haga clic en **Aceptar** para ejecutar el comando Detach.  
  
5.  Busque la carpeta **bases de datos** en el panel izquierdo o derecho de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] .  
  
6.  Haga clic con el botón secundario en la carpeta **bases** de datos y seleccione **adjuntar..** .  
  
7.  En el cuadro de texto **Carpeta** , escriba la ubicación original de la carpeta de la base de datos. Como alternativa, puede usar el botón Examinar (**...**) para buscar la carpeta de la base de datos.  
  
8.  Seleccione el modo de lectura/escritura para la base de datos.  
  
9. Escriba la contraseña que se usó en el paso 3 y haga clic en **Aceptar** para ejecutar el comando adjuntar.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-programmatically-using-amo"></a>Para cambiar el modo de lectura/escritura de una base de datos mediante programación a través de AMO  
  
1.  En la aplicación C#, adapte el código de ejemplo siguiente y complete las tareas indicadas.  
  
 `private void SwitchReadWrite(Server server, string dbName,`  
  
 `ReadWriteMode dbReadWriteMode)`  
  
 `{`  
  
 `if (server.Databases.ContainsName(dbName))`  
  
 `{`  
  
 `Database db;`  
  
 `string databaseLocation;`  
  
 `db = server.Databases[dbName];`  
  
 `databaseLocation = db.DbStorageLocation;`  
  
 `if (databaseLocation == null)`  
  
 `{`  
  
 `string dataDir = server.ServerProperties["DataDir"].Value;`  
  
 `String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);`  
  
 `if (possibleFolders.Length > 1)`  
  
 `{`  
  
 `List<String> sortedFolders = new List<string>(possibleFolders.Length);`  
  
 `sortedFolders.AddRange(possibleFolders);`  
  
 `sortedFolders.Sort();`  
  
 `databaseLocation = sortedFolders[sortedFolders.Count - 1];`  
  
 `}`  
  
 `else`  
  
 `{`  
  
 `databaseLocation = possibleFolders[0];`  
  
 `}`  
  
 `}`  
  
 `db.Detach();`  
  
 `server.Attach(databaseLocation, dbReadWriteMode);`  
  
 `}`  
  
 `}`  
  
1.  En la aplicación C#, invoque `SwitchReadWrite()` con los parámetros necesarios.  
  
2.  Compile y ejecute el código para mover la base de datos.  
  
#### <a name="to-switch-the-readwrite-mode-to-a-database-by-script-using-xmla"></a>Para cambiar el modo de lectura/escritura de una base de datos mediante script XMLA  
  
1.  Localice la base de datos en el panel izquierdo o derecho de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Haga clic con el botón secundario en la base de datos y seleccione **propiedades**. Busque la carpeta de la base de datos y anote su ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
    > [!IMPORTANT]  
    >  En cuanto se separa la base de datos, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ya no puede ayudarle a obtener su ubicación.  
  
3.  Abra una nueva pestaña XMLA en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copie la plantilla de script siguiente para XMLA:  
  
 `<Detach xmlns="https://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Reemplace `%dbName%` por el nombre de la base de datos y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
3.  Copie la plantilla de script siguiente para XMLA en una nueva pestaña XMLA  
  
 `<Attach xmlns="https://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="https://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Reemplace `%dbFolder%` por la ruta UNC completa de la carpeta de la base de datos, `%ReadOnlyMode%` por el valor `ReadOnly` o `ReadWrite` correspondiente, y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
## <a name="see-also"></a>Consulte también  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 [Microsoft. AnalysisServices. Database. Detach *](/dotnet/api/microsoft.analysisservices.core.database.detach)   
 [Adjuntar y separar bases de datos de Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Ubicación de almacenamiento de base de datos](database-storage-location.md)   
 [Base de datos Readwritemode](database-readwritemodes.md)   
 [Elemento Attach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/attach-element)   
 [Elemento detach](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/detach-element)   
 [Elemento ReadWriteMode](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/readwritemode-element)   
 [Elemento DbStorageLocation](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/dbstoragelocation-element)  
  
  
