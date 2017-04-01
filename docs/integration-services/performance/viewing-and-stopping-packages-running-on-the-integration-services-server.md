---
title: "Ver y detener los paquetes en ejecuci&#243;n en el Servidor de Integration Services | Microsoft Docs"
ms.custom: ""
ms.date: "08/26/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "paquetes [Integration Services], administración"
  - "administrar paquetes en ejecución [Integration Services]"
  - "paquetes [Integration Services], ejecución"
  - "paquetes en ejecución [Integration Services], administración"
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
caps.latest.revision: 18
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 18
---
# Ver y detener los paquetes en ejecuci&#243;n en el Servidor de Integration Services
  La base de datos de **SSISDB** almacena el historial de ejecuciones en tablas internas que no son visibles para los usuarios. Sin embargo, expone la información que necesita a través de vistas públicas que puede consultar. También proporciona procedimientos almacenados a los que puede llamar para realizar tareas frecuentes relacionadas con los paquetes.  
  
 Normalmente, administra los objetos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] del servidor en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Sin embargo, también puede consultar las vistas de base de datos y llamar a los procedimientos almacenados directamente, o escribir código personalizado que llame a la API administrada. [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] y la API administrada consultan las vistas y llaman a los procedimientos almacenados para realizar muchas de sus tareas. Por ejemplo, puede ver la lista de paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se están ejecutando actualmente en el servidor y solicitar que se detengan si es necesario.  
  
## Ver la lista de paquetes en ejecución  
 Puede ver la lista de paquetes que hay en ejecución actualmente en el servidor en el cuadro de diálogo **Operaciones activas** . Para más información, consulte [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Para obtener información sobre los demás métodos que puede usar para ver la lista de paquetes en ejecución, vea los siguientes temas.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 Para ver la lista de los paquetes que se están ejecutando en el servidor, consulte la vista [catalog.executions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md) para los paquetes que tengan un estado de 2.  
  
 Acceso mediante programación a través de la API administrada  
 Consulte el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## Detener un paquete en ejecución  
 En el cuadro de diálogo **Operaciones activas** , puede solicitar que se detenga un paquete en ejecución. Para más información, consulte [Active Operations Dialog Box](../../integration-services/performance/active-operations-dialog-box.md).  
  
 Para obtener información acerca de los otros métodos que puede usar para detener un paquete en ejecución, vea los temas siguientes.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 Para detener un paquete en ejecución en el servidor, llame al procedimiento almacenado [catalog.stop_operation &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database.md).  
  
 Acceso mediante programación a través de la API administrada  
 Consulte el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## Ver el historial de paquetes ejecutados  
 Para ver el historial de los paquetes que se han ejecutado en [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)], use el informe **Todas las ejecuciones** . Para obtener más información sobre el informe **Todas las ejecuciones** y otros informes estándar, vea [Informes para el servidor de Integration Services](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
 Para obtener información acerca de los demás métodos que puede usar para ver el historial de paquetes en ejecución, vea los siguientes temas.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] access  
 Para ver información sobre los paquetes que se han ejecutado, consulte la vista [catalog.executions &#40;base de datos de SSISDB&#41;](../../integration-services/system-views/catalog-executions-ssisdb-database.md).  
  
 Acceso mediante programación a través de la API administrada  
 Consulte el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## Vea también  
 [Ejecución de proyectos y paquetes](https://msdn.microsoft.com/library/hh213290.aspx)   
 [Solucionar problemas de informes para la ejecución de paquetes](https://msdn.microsoft.com/library/gg471512.aspx)  
  
  