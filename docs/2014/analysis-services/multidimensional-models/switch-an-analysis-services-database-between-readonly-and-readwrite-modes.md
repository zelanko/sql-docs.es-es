---
title: Cambiar una base de datos de Analysis Services entre los modos ReadOnly y ReadWrite | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- ReadOnly property
- ReadWriteMode command
- operations [Analysis Services - multidimensional data]
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b2f9b97122e157ffd356163de63b0ab96708f36a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48178205"
---
# <a name="switch-an-analysis-services-database-between-readonly-and-readwrite-modes"></a>Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services
  A menudo hay situaciones cuando un [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] Administrador de base de datos (dba) desea cambiar el modo de lectura/escritura de una base de datos tabular o multidimensional. Estas situaciones suelen responder a necesidades empresariales, como compartir la base de datos entre un grupo de servidores de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para proporcionar una mejor experiencia para el usuario.  
  
 El modo de una base de datos se puede cambiar de muchas formas. En este documento se describen los siguientes escenarios comunes:  
  
-   Usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usar programación a través de AMO  
  
-   Usar script XMLA  
  
## <a name="procedures"></a>Procedimientos  
  
#### <a name="to-switch-the-readwrite-mode-of-a-database-interactively-using-management-studio"></a>Para cambiar el modo de lectura/escritura de una base de datos de forma interactiva mediante Management Studio  
  
1.  Localice la base de datos en el panel izquierdo o derecho de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
2.  Haga clic en la base de datos y seleccione **propiedades**. Busque la carpeta de la base de datos y anote su ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
    > [!IMPORTANT]  
    >  En cuanto se separa la base de datos, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ya no puede ayudarle a obtener su ubicación.  
  
3.  Haga clic con el botón derecho en la base de datos y seleccione **Separar…**  
  
4.  Asigne una contraseña a la base de datos que se va separar y, a continuación, haga clic en **Aceptar** para ejecutar el comando Detach.  
  
5.  Busque el **bases de datos** carpeta en el panel izquierdo o derecho de [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
6.  Haga clic en el **bases de datos** carpeta y seleccione **adjuntar...**  
  
7.  En el cuadro de texto **Carpeta** , escriba la ubicación original de la carpeta de la base de datos. También puede usar el botón Examinar (**…**) para buscar la carpeta de la base de datos.  
  
8.  Seleccione el modo de lectura/escritura para la base de datos.  
  
9. Escriba la contraseña que utilizó en el paso 3 y haga clic en **Aceptar** para ejecutar el comando attach.  
  
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
  
2.  Haga clic en la base de datos y seleccione **propiedades**. Busque la carpeta de la base de datos y anote su ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
    > [!IMPORTANT]  
    >  En cuanto se separa la base de datos, [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] ya no puede ayudarle a obtener su ubicación.  
  
3.  Abra una nueva pestaña XMLA en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copie la plantilla de script siguiente para XMLA:  
  
 `<Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">`  
  
 `<Object>`  
  
 `<DatabaseID>%dbName%</DatabaseID>`  
  
 `<Password>%password%</Password>`  
  
 `</Object>`  
  
 `</Detach>`  
  
1.  Reemplace `%dbName%` por el nombre de la base de datos y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
3.  Copie la plantilla de script siguiente para XMLA en una nueva pestaña XMLA  
  
 `<Attach xmlns="http://schemas.microsoft.com/analysisservices/2003` `/engine` `">`  
  
 `<Folder>%dbFolder%</Folder>`  
  
 `<ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>`  
  
 `</Attach>`  
  
1.  Reemplace `%dbFolder%` por la ruta UNC completa de la carpeta de la base de datos, `%ReadOnlyMode%` por el valor `ReadOnly` o `ReadWrite` correspondiente, y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
2.  Ejecute el comando XMLA.  
  
## <a name="see-also"></a>Vea también  
 <xref:Microsoft.AnalysisServices.Server.Attach%2A>   
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Adjuntar y separar bases de datos de Analysis Services](attach-and-detach-analysis-services-databases.md)   
 [Ubicación de almacenamiento de base de datos](database-storage-location.md)   
 [ReadWriteModes de base de datos](database-readwritemodes.md)   
 [Elemento Attach](../xmla/xml-elements-commands/attach-element.md)   
 [Elemento Detach](../xmla/xml-elements-commands/detach-element.md)   
 [Elemento ReadWriteMode](../xmla/xml-elements-properties/readwritemode-element.md)   
 [Elemento DbStorageLocation](../xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  
