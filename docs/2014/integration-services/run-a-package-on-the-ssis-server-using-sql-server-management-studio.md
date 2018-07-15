---
title: Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 56dc1bf8-99d4-41dc-bdc4-f64f1ccfd688
caps.latest.revision: 8
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 58348805f20f33124e0a789c79aa2ef71f9d8793
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37225555"
---
# <a name="run-a-package-on-the-ssis-server-using-sql-server-management-studio"></a>Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio
  Después de implementar el proyecto en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , puede ejecutar el paquete en el servidor.  
  
 Puede utilizar los informes de operaciones para ver información sobre los paquetes que se han ejecutado, o que se están ejecutando actualmente, en el servidor. Para obtener más información, consulte [Reports for the Integration Services Server](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
### <a name="to-run-a-package-on-the-server-using-sql-server-management-studio"></a>Para ejecutar un paquete en el servidor con SQL Server Management Studio  
  
1.  Abra [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y conéctese a la instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que contiene el catálogo de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
2.  En el Explorador de objetos, expanda el nodo **Catálogos de Integration Services** , expanda el nodo **SSISDB** y vaya al paquete contenido en el proyecto que ha implementado.  
  
3.  Haga clic con el botón derecho en el nombre del paquete y seleccione **Ejecutar**.  
  
4.  Configure la ejecución del paquete mediante las opciones de las pestañas **Parámetros**, **Administradores de conexión**y **Avanzadas** del cuadro de diálogo **Ejecutar paquete** .  
  
5.  Haga clic en **Aceptar** para ejecutar el paquete.  
  
     -o bien-  
  
     Utilice procedimientos almacenados para ejecutar el paquete. Haga clic en **Script** para generar la instrucción Transact-SQL que crea una instancia de la ejecución y la inicia. La instrucción incluye una llamada a los procedimientos almacenados catalog.create_execution, catalog.set_execution_parameter_value y catalog.start_execution. Para obtener más información sobre estos procedimientos almacenados, vea [catalog.create_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-create-execution-ssisdb-database), [catalog.set_execution_parameter_value &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-set-execution-parameter-value-ssisdb-database) y [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database).  
  
  
