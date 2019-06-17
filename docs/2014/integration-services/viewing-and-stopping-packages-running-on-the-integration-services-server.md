---
title: Ver y detener los paquetes que se ejecutan en la integración de servicios de servidor | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- packages [Integration Services], managing
- managing running packages [Integration Services]
- packages [Integration Services], running
- running package [Integration Services], managing
ms.assetid: 11bf44e6-f6b0-475f-b816-40e914dbac80
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 9a53cf3dbd11c87177c725cf246fb4b1016d87ed
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66054597"
---
# <a name="viewing-and-stopping-packages-running-on-the-integration-services-server"></a>Ver y detener los paquetes en ejecución en el Servidor de Integration Services
  La base de datos de `SSISDB` almacena el historial de ejecuciones en tablas internas que no son visibles para los usuarios. Sin embargo, expone la información que necesita a través de vistas públicas que puede consultar. También proporciona procedimientos almacenados a los que puede llamar para realizar tareas frecuentes relacionadas con los paquetes.  
  
 Normalmente, administra los objetos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] del servidor en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Sin embargo, también puede consultar las vistas de base de datos y llamar a los procedimientos almacenados directamente, o escribir código personalizado que llame a la API administrada. [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] y la API administrada consultan las vistas y llaman a los procedimientos almacenados para realizar muchas de sus tareas. Por ejemplo, puede ver la lista de paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que se están ejecutando actualmente en el servidor y solicitar que se detengan si es necesario.  
  
## <a name="viewing-the-list-of-running-packages"></a>Ver la lista de paquetes en ejecución  
 Puede ver la lista de paquetes que hay en ejecución actualmente en el servidor en el cuadro de diálogo **Operaciones activas** . Para más información, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obtener información sobre los demás métodos que puede usar para ver la lista de paquetes en ejecución, vea los siguientes temas.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] access  
 Para ver la lista de los paquetes que se están ejecutando en el servidor, consulte la vista [catalog.executions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database) para los paquetes que tengan un estado de 2.  
  
 Acceso mediante programación a través de la API administrada  
 Vea el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## <a name="stopping-a-running-package"></a>Detener un paquete en ejecución  
 En el cuadro de diálogo **Operaciones activas** , puede solicitar que se detenga un paquete en ejecución. Para más información, consulte [Active Operations Dialog Box](../../2014/integration-services/active-operations-dialog-box.md).  
  
 Para obtener información acerca de los otros métodos que puede usar para detener un paquete en ejecución, vea los temas siguientes.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] access  
 Para detener un paquete en ejecución en el servidor, llame al procedimiento almacenado [catalog.stop_operation &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-stop-operation-ssisdb-database).  
  
 Acceso mediante programación a través de la API administrada  
 Vea el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## <a name="viewing-the-history-of-packages-that-have-run"></a>Ver el historial de paquetes ejecutados  
 Para ver el historial de los paquetes que se han ejecutado en [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)], use el informe **Todas las ejecuciones** . Para obtener más información sobre el informe **Todas las ejecuciones** y otros informes estándar, vea [Informes para el servidor de Integration Services](../../2014/integration-services/reports-for-the-integration-services-server.md).  
  
 Para obtener información acerca de los demás métodos que puede usar para ver el historial de paquetes en ejecución, vea los siguientes temas.  
  
 [!INCLUDE[tsql](../includes/tsql-md.md)] access  
 Para ver información sobre los paquetes que se han ejecutado, consulte la vista [catalog.executions &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-executions-ssisdb-database).  
  
 Acceso mediante programación a través de la API administrada  
 Vea el espacio de nombres <xref:Microsoft.SqlServer.Management.IntegrationServices> y sus clases.  
  
## <a name="see-also"></a>Vea también  
 [Ejecución de proyectos y paquetes](packages/run-integration-services-ssis-packages.md)   
 [Solucionar problemas de informes para la ejecución de paquetes](troubleshooting/troubleshooting-reports-for-package-execution.md)  
  
  
