---
title: Supervisión de ejecuciones de paquetes y otras operaciones | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: cbbcd79f-ab9b-46ec-84cb-4821c1d16b99
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 628b62d9c8e01d0dc0bf641551de67c3838a4504
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85423252"
---
# <a name="monitoring-for-package-executions-and-other-operations"></a>Supervisar las ejecuciones de paquetes y otras operaciones
  Puede supervisar las ejecuciones de paquetes [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , validaciones de proyectos y otras operaciones mediante una o varias de las herramientas siguientes. Algunas herramientas como las derivaciones de datos solo están disponibles para los proyectos que se implementan en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] .  
  
-   Registros  
  
     Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](integration-services-ssis-logging.md).  
  
-   Informes  
  
     Para obtener más información, consulte [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md).  
  
-   Vistas  
  
     Para obtener más información, vea [Vistas &#40;catálogo de Integration Services&#41;](/sql/integration-services/system-views/views-integration-services-catalog).  
  
-   Contadores de rendimiento  
  
     Para más información, consulte [Performance Counters](performance-counters.md).  
  
-   Derivaciones de datos  
  
## <a name="operation-types"></a>Tipos de operación  
 En el catálogo de `SSISDB` se supervisan varios tipos diferentes de operaciones, en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cada operación puede tener varios mensajes asociados. Cada mensaje se puede clasificar en uno de varios tipos. Por ejemplo, un mensaje puede ser de información, de advertencia o de error. Para obtener la lista completa de tipos de mensaje, vea la documentación de la vista [catalog.operation_messages &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operation-messages-ssisdb-database) de Transact-SQL. Para obtener una lista completa de los tipos de operaciones, vea [catalog.operations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
 Se usan nueve tipos de estado diferentes para indicar el estado de una operación. Para obtener una lista completa de los tipos de estado, vea la vista [catalog.operations &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-views/catalog-operations-ssisdb-database).  
  
## <a name="related-content"></a>Contenido relacionado  
 Entrada de blog con una [introducción a la API T-SQL de SSIS](https://go.microsoft.com/fwlink/?LinkId=249051), en blogs.msdn.com.  
  
  
