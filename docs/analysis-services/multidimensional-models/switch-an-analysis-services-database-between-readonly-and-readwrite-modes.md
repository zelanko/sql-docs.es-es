---
title: "Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/06/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "ReadOnly, propiedad"
  - "ReadWriteMode, comando"
  - "operaciones [Analysis Services - datos multidimensionales]"
ms.assetid: 4eff8181-08dd-4fad-b091-d400fc21a020
caps.latest.revision: 16
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 16
---
# Cambiar entre los modos ReadOnly y ReadWrite en una base de datos de Analysis Services
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] los administradores de base de datos pueden cambiar el modo de lectura y escritura de una base de datos multidimensional o tabular como parte de un esfuerzo mayor que distribuye una carga de trabajo de consultas entre varios servidores de solo consulta.  
  
 El modo de una base de datos se puede cambiar de varias formas. En este documento se describen los siguientes escenarios comunes:  
  
-   Usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]  
  
-   Usar programación a través de AMO  
  
-   Script con XMLA o TMSL  
  
## Cambio del modo de lectura/escritura de una base de datos de forma interactiva mediante Management Studio  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos y seleccione **Propiedades**.  
  
     Tenga en cuenta la ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
2.  Haga clic con el botón derecho en la base de datos y seleccione **Separar…**  
  
3.  Asigne una contraseña a la base de datos que se va separar y, a continuación, haga clic en **Aceptar** para ejecutar el comando Detach.  
  
4.  En el Explorador de objetos, haga clic con el botón derecho en la carpeta **Bases de datos** y, después, seleccione **Asociar…**  
  
5.  En el cuadro de texto **Carpeta** , escriba la ubicación original de la carpeta de la base de datos. También puede usar el botón Examinar (**…**) para buscar la carpeta de la base de datos.  
  
6.  Seleccione el modo de lectura/escritura para la base de datos.  
  
7.  Escriba la contraseña y haga clic en **Aceptar** para ejecutar el comando Attach.  
  
## Cambio del modo de lectura/escritura de una base de datos mediante programación a través de AMO  
 En la aplicación C#, invoque `SwitchReadWrite()` con los parámetros necesarios. Compile y ejecute el código para mover la base de datos.  
  
```  
private void SwitchReadWrite(Server server, string dbName, ReadWriteMode dbReadWriteMode)  
{  
    if (server.Databases.ContainsName(dbName))  
    {  
        Database db;  
        string databaseLocation;  
        db = server.Databases[dbName];  
        databaseLocation = db.DbStorageLocation;  
  
              if (databaseLocation == null)  
            {  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
                 string dataDir = server.ServerProperties["DataDir"].Value;  
  
    String[] possibleFolders = Directory.GetDirectories(dataDir, string.Concat(dbName,"*"), SearchOption.TopDirectoryOnly);  
  
   if (possibleFolders.Length > 1)  
         {  
         List<String> sortedFolders = new List<string>(possibleFolders.Length);  
         sortedFolders.AddRange(possibleFolders);  
         sortedFolders.Sort();  
         databaseLocation = sortedFolders[sortedFolders.Count - 1];  
         }  
         else  
         {  
         databaseLocation = possibleFolders[0];  
          }  
        }  
    db.Detach();  
    server.Attach(databaseLocation, dbReadWriteMode);  
    }  
}  
  
```  
  
## Cambio del modo de lectura/escritura de una base de datos mediante script XMLA  
 Las instrucciones siguientes se aplican a las bases de datos multidimensionales y tabulares en modo de compatibilidad de 1050, 1100 o 1103.  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la base de datos y seleccione **Propiedades**.  
  
     Tenga en cuenta la ubicación. Una ubicación de almacenamiento de la base de datos vacía indica que la carpeta de la base de datos está ubicada en la carpeta de datos del servidor.  
  
2.  Haga clic con el botón derecho en la base de datos y seleccione **Separar…**  
  
3.  Abra una nueva pestaña XMLA en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
4.  Copie la plantilla de script siguiente para XMLA:  
  
    ```  
    <Detach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Object>  
          <DatabaseID>%dbName%</DatabaseID>  
          <Password>%password%</Password>  
       </Object>  
    </Detach>  
    ```  
  
5.  Reemplace `%dbName%` por el nombre de la base de datos y `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
6.  Ejecute el comando XMLA.  
  
7.  Copie la plantilla de script siguiente para XMLA en una nueva pestaña XMLA  
  
    ```  
    <Attach xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
       <Folder>%dbFolder%</Folder>  
       <ReadWriteMode xmlns="http://schemas.microsoft.com/analysisservices/2008/engine/100">%ReadOnlyMode%</ReadWriteMode>  
    </Attach>  
    ```  
  
8.  Reemplace `%dbFolder%` por la ruta de acceso UNC completa de la carpeta de la base de datos, `%ReadOnlyMode%` por el valor **ReadOnly** o **ReadWrite** correspondiente y, por último, `%password%` por la contraseña. Los caracteres % forman parte de la plantilla y se deben quitar.  
  
9. Ejecute el comando XMLA.  
  
## Vea también  
 <xref:Microsoft.AnalysisServices.Database.Detach%2A>   
 [Alta disponibilidad y escalabilidad en Analysis Services](../../analysis-services/instances/high-availability-and-scalability-in-analysis-services.md)   
 [Adjuntar y separar bases de datos de Analysis Services](../../analysis-services/multidimensional-models/attach-and-detach-analysis-services-databases.md)   
 [Ubicación de almacenamiento de las bases de datos](../../analysis-services/multidimensional-models/database-storage-location.md)   
 [Modos de la propiedad de base de datos ReadWriteMode](../../analysis-services/multidimensional-models/database-readwritemodes.md)   
 [Elemento Attach](../../analysis-services/xmla/xml-elements-commands/attach-element.md)   
 [Elemento Detach](../../analysis-services/xmla/xml-elements-commands/detach-element.md)   
 [Elemento ReadWriteMode](../../analysis-services/xmla/xml-elements-properties/readwritemode-element.md)   
 [Elemento DbStorageLocation](../../analysis-services/xmla/xml-elements-properties/dbstoragelocation-element.md)  
  
  