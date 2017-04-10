---
title: "Lecci&#243;n 2: Especificar informaci&#243;n de conexi&#243;n (Reporting Services) | Microsoft Docs"
ms.custom: ""
ms.date: "05/23/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
caps.handback.revision: 51
---
# Lecci&#243;n 2: Especificar informaci&#243;n de conexi&#243;n (Reporting Services)
Después de agregar un informe al proyecto Tutorial, necesita definir un *origen de datos*, que es la información de conexión que el informe usa para tener acceso a los datos procedentes de una base de datos relacional, una base de datos multidimensional u otro recurso.  
  
En esta lección usará la base de datos de ejemplo [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] como origen de datos. En este tutorial se da por hecho que esta base de datos se encuentra en una instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)], que está instalada en el equipo local.  
  
### Para configurar una conexión  
  
1.  En el panel **Datos de informe**, haga clic en **Nuevo** y, después, en **Origen de datos**.  
Si el panel **Datos de informe** no está visible, haga clic en **Datos de informe** en el menú **Ver**.  
  
   2.  En **Nombre**, escriba *Adventureworks2014*.  
  
3.  Asegúrese de que está seleccionado **Conexión incrustada**.  
  
4.  En **Tipo**, seleccione **Microsoft SQL Server**.  
  
5.  En **Cadena de conexión**, escriba lo siguiente:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
Esta cadena de conexión da por supuesto que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el servidor de informes y la base de datos [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] están instalados en el equipo local, y que el usuario tiene permiso para iniciar una sesión en la base de datos [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]. Si la base de datos AdventureWorks2014 no está en el equipo local, cambie la cadena de conexión y reemplace *localhost* con el nombre de la instancia del servidor de base de datos.
   
  
 > [!NOTE]  
 > Si utiliza [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services o una instancia con nombre, la cadena de conexión debe incluir información de la instancia:  
 >   
 > `Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
 >   
 > Para obtener más información sobre cadenas de conexión, consulte:  
 > *  [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
    > * [Propiedades del origen de datos (cuadro de diálogo), General](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
        
  
6.  Haga clic en **Credenciales** en el panel izquierdo y haga clic en **Usar autenticación de Windows (seguridad integrada)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] El origen de datos [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] se agrega al panel **Datos de informe**.  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## Tarea siguiente  
Ha definido correctamente una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)]. A continuación, creará el informe. Consulte la [Lección 3: Definir un conjunto de datos para el informe de tabla &#40;Reporting Services&#41;;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## Vea también  
[Propiedades del origen de datos (cuadro de diálogo), General](../Topic/Data%20Source%20Properties%20Dialog%20Box,%20General.md)  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  
