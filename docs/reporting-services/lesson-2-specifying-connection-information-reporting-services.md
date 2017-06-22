---
title: "Lección 2: Especificar información de conexión (Reporting Services) | Documentos de Microsoft"
ms.custom: 
ms.date: 05/23/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to:
- SQL Server 2016
ms.assetid: 54405a3a-d7fa-4d95-8963-9aa224e5901e
caps.latest.revision: 53
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 4d0667dec1b59d5560ca24176634dddc5d6d8d18
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-2-specifying-connection-information-reporting-services"></a>Lección 2: Especificar información de conexión (Reporting Services)
Después de agregar un [!INCLUDE[ssRSnoversion_md](../includes/ssrsnoversion-md.md)] paginados informe al proyecto de Tutorial en la lección 1, ahora tiene que definir un *origen de datos*, que es la información de conexión, el informe utiliza para tener acceso a datos desde una base de datos relacional, base de datos multidimensional u otro origen.  
  
En esta lección, utilizará el [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] base de datos de ejemplo como origen de datos. Este tutorial se da por supuesto que esta base de datos se encuentra en una instancia predeterminada de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)] instalada en el equipo local.  
  
### <a name="to-set-up-a-connection"></a>Para configurar una conexión  
  
1.  En el panel **Datos de informe** , haga clic en **Nuevo** y, después, en **Data Source**.  
Si el panel **Datos de informe** no está visible, haga clic en **Datos de informe** en el menú **Ver**.  

    ![SSRS-Table-tutorial-2-New-Data-Source](../reporting-services/media/ssrs-table-tutorial-2-new-data-source.png)
  
   2.  En **Nombre**, escriba *AdventureWorks2014*.  
  
3.  Asegúrese de que está seleccionado **Conexión incrustada** .  
  
4.  En **Tipo**, seleccione **Microsoft SQL Server**.  
  
5.  En **Cadena de conexión**, escriba lo siguiente:  
  
    ```  
    Data source=localhost; initial catalog=AdventureWorks2014  
    ```  
  
     Esta cadena de conexión da por supuesto que [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], el servidor de informes y la base de datos [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] están instalados en el equipo local, y que el usuario tiene permiso para iniciar una sesión en la base de datos [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . Si la base de datos AdventureWorks2014 no está en el equipo local, cambie la cadena de conexión y reemplace *localhost* con el nombre de la instancia de servidor de base de datos.
  
     >[!NOTE]  
    >Si utiliza [!INCLUDE[ssExpress](../includes/ssexpress-md.md)] con Advanced Services o una instancia con nombre, la cadena de conexión debe incluir información de la instancia:  
    >  
    >`Data source=localhost\SQLEXPRESS; initial catalog=AdventureWorks2014`  
    >  
    >Para obtener más información sobre cadenas de conexión, consulte: [Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
     
  
6.  Haga clic en **Credenciales** en el panel izquierdo y haga clic en **Usar autenticación de Windows (seguridad integrada)**.  
  
7.  [!INCLUDE[clickOK](../includes/clickok-md.md)] El origen de datos **AdventureWorks2014** se agrega al panel **Datos de informe** .  
![ssrs_adventureworks_datasource](../reporting-services/media/ssrs-adventureworks-datasource.png)  
## <a name="next-task"></a>Tarea siguiente  
Ha definido correctamente una conexión a la base de datos de ejemplo [!INCLUDE[ssSampleDBAdventureworks2014_md](../includes/sssampledbadventureworks2014-md.md)] . A continuación, creará el informe. Consulte la [Lección 3: Definir un conjunto de datos para el informe de tabla &#40;Reporting Services&#41;;](../reporting-services/lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md).  
  
## <a name="see-also"></a>Vea también  
[Data Connections, Data Sources, and Connection Strings in Reporting Services](../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md)  
  
  
  


