---
title: Realizar copias de seguridad de bases de datos de DQS y restaurarlas
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: data-quality-services
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: f3091f62-2234-4a80-a615-cf14c2a1da85
author: swinarko
ms.author: sawinark
ms.openlocfilehash: 94b2529323e5a075b6fd423fd8c69ece7a0535c0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75258851"
---
# <a name="backing-up-and-restoring-dqs-databases"></a>Realizar copias de seguridad de bases de datos de DQS y restaurarlas

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

  En este tema se describe cómo realizar copias de seguridad de las bases de datos de DQS y cómo restaurarlas.  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="prerequisites"></a><a name="Prerequisites"></a> Requisitos previos  
  
-   Debe saber o recordar la contraseña de la clave maestra de base de datos que proporcionó durante la instalación del servidor DQS.  
  
-   Asegúrese de que no haya actividades o procesos de DQS en ejecución. Utilice la pantalla **Supervisión de actividades** para comprobarlo. Para obtener información detallada sobre cómo utilizar esta pantalla, vea [Monitor DQS Activities](../data-quality-services/monitor-dqs-activities.md).  
  
-   Asegúrese de que ningún usuario haya iniciado sesión en el servidor DQS.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
  
-   La cuenta de usuario de Windows debe ser miembro del rol fijo de servidor sysadmin en la instancia de SQL Server para realizar las operaciones de copia de seguridad y restauración.  
  
-   Debe disponer del rol dqs_administrator en la base de datos DQS_MAIN para terminar las actividades o detener los procesos en ejecución en DQS.  
  
##  <a name="backup-and-restore-dqs-databases"></a><a name="BackupRestore"></a>Copia de seguridad y restauración de bases de datos de DQS  
  
1.  Inicie Microsoft SQL Server Management Studio y conéctese a la instancia adecuada de SQL Server.  
  
2.  En el Explorador de objetos, expanda el nodo **Bases de datos** .  
  
3.  Haga una copia de seguridad de la base de datos DQS_STAGING_DATA. Para obtener instrucciones paso a paso sobre cómo realizar una copia de seguridad de una base de datos de SQL Server, vea [Crear una copia de seguridad completa de base de datos &#40;SQL Server&#41;](../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md).  
  
4.  Haga una copia de seguridad de la base de datos DQS_PROJECTS.  
  
5.  Haga una copia de seguridad de la base de datos DQS_MAIN.  
  
6.  Desconéctese de la instancia actual de SQL Server y conéctese a la instancia de SQL Server donde desea restaurar estas bases de datos.  
  
7.  Restaure la base de datos DQS_MAIN. Para obtener instrucciones paso a paso sobre cómo restaurar una base de datos de SQL Server, vea [Restaurar una copia de seguridad de base de datos con SSMS](../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md).  
  
8.  Restaure la base de datos DQS_PROJECTS.  
  
9. Restaure la base de datos DQS_STAGING_DATA.  
  
10. En el Explorador de objetos, haga clic con el botón secundario en el servidor y, a continuación, haga clic en **Nueva consulta**.  
  
11. En la ventana Editor de consultas, copie las instrucciones SQL siguientes y reemplace * \<>de contraseña* por la contraseña que proporcionó durante la instalación de DQS para la clave maestra de base de datos:  
  
    ```  
    USE [DQS_MAIN]  
    GO  
    EXECUTE [internal_core].[RestoreDQDatabases] '<PASSWORD>'  
    GO  
  
    ```  
  
12. Presione F5 para ejecutar las instrucciones. Vea el panel **Resultados** para comprobar que las instrucciones se han ejecutado correctamente.  
  
## <a name="see-also"></a>Consulte también  
 [Manage DQS Databases](../data-quality-services/manage-dqs-databases.md)  
  
  
