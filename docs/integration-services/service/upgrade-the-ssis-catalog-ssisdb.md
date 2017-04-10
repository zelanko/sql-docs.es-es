---
title: "Actualizaci&#243;n del cat&#225;logo de SSIS (SSISDB) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.ssis.dbupgradewizard.f1"
ms.assetid: 170c3dc9-f5bf-4599-ae56-d24a620f23e8
caps.latest.revision: 8
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 8
---
# Actualizaci&#243;n del cat&#225;logo de SSIS (SSISDB)
  Ejecute el Asistente para actualización de SSISDB para actualizar la base de datos del catálogo de SSIS, SSISDB, cuando esta sea anterior a la versión actual de la instancia de SQL Server. Tiene lugar cuando se presenta alguna de las siguientes condiciones.  
  
-   Restauró la base de datos de una versión anterior de SQL Server.  
  
-   No ha quitado la base de datos de un grupo de disponibilidad AlwaysOn antes de actualizar la instancia de SQL Server. Esto evita la actualización automática de la base de datos. Para obtener más información, vea [Upgrading SSISDB in an availability group](../../integration-services/service/always-on-for-ssis-catalog-ssisdb.md#Upgrade).  
  
 El asistente solo puede actualizar la base de datos en una instancia de servidor local.  
  
## Actualización del catálogo de SSIS (SSISDB) mediante la ejecución del Asistente para actualización de SSISDB  
  
1.  Copia de seguridad de la base de datos Catálogo de SSIS, SSISDB.  
  
2.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], expanda el servidor local y luego expanda **Catálogos de Integration Services**.  
  
3.  Haga clic con el botón derecho en **SSISDB** y, después, seleccione **Actualización de base de datos** para iniciar el Asistente para actualización de SSISDB.  
  
     ![Launch the SSISDB upgrade wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-1.png "Launch the SSISDB upgrade wizard")  
  
4.  En la página **Seleccionar instancia** , seleccione una instancia de SQL Server en el servidor local.  
  
    > [!IMPORTANT]  
    >  El asistente solo puede actualizar la base de datos en una instancia de servidor local.  
  
     Active la casilla para indicar que ha realizado la copia de seguridad de la base de datos SSISDB antes de ejecutar al asistente.  
  
     ![Select the server in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-2.png "Select the server in the SSISDB Upgrade Wizard")  
  
5.  Seleccione **Actualizar** para actualizar la base de datos Catálogo de SSIS.  
  
6.  En la página **Resultado** , examine los resultados.  
  
     ![Review the results in the SSISDB Upgrade Wizard](../../integration-services/service/media/ssisdb-upgrade-wizard-3.png "Review the results in the SSISDB Upgrade Wizard")  
  
  