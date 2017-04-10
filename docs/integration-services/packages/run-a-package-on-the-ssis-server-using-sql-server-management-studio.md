---
title: "Ejecutar un paquete en el Servidor SSIS con SQL Server Management Studio | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
caps.latest.revision: 9
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 9
---
# Ejecutar un paquete en el Servidor SSIS con SQL Server Management Studio
  Después de implementar el proyecto en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede ejecutar el paquete en el servidor.  
  
 Puede utilizar los informes de operaciones para ver información sobre los paquetes que se han ejecutado, o que se están ejecutando actualmente, en el servidor. Para obtener más información, consulte [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
### Para ejecutar un paquete en el servidor con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contiene el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de objetos, expanda el nodo **Catálogos de Integration Services** , expanda el nodo **SSISDB** y vaya al paquete contenido en el proyecto que ha implementado.  
  
3.  Haga clic con el botón derecho en el nombre del paquete y seleccione **Ejecutar**.  
  
4.  Configure la ejecución del paquete mediante las opciones de las pestañas **Parámetros**, **Administradores de conexión**y **Avanzadas** del cuadro de diálogo **Ejecutar paquete** .  
  
5.  Haga clic en **Aceptar** para ejecutar el paquete.  
  
     - O bien -  
  
     Utilice procedimientos almacenados para ejecutar el paquete. Haga clic en **Script** para generar la instrucción Transact-SQL que crea una instancia de la ejecución y la inicia. La instrucción incluye una llamada a los procedimientos almacenados catalog.create_execution, catalog.set_execution_parameter_value y catalog.start_execution. Para obtener más información sobre estos procedimientos almacenados, vea [catalog.create_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database.md), [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database.md) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md).  
  
  