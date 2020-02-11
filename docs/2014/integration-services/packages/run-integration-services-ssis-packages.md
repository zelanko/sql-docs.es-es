---
title: Ejecución de proyectos y paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Integration Services packages, running
- SSIS packages, running
- packages [Integration Services], running
- SQL Server Integration Services packages, running
- executing packages [Integration Services]
- running packages [Integration Services]
- Integration Services, (See also Integration Services packages)
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 5a3ecbe615d60a703b66dff78cd77ddfde0a20d1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62767095"
---
# <a name="execution-of-projects-and-packages"></a>Ejecución de proyectos y paquetes
  Para ejecutar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede utilizar una de las herramientas en función de dónde se almacenan los paquetes. Las herramientas se enumeran en la tabla a continuación.  
  
 Para almacenar un paquete en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , utilice el modelo de implementación del proyecto para implementar el proyecto en el servidor. Para obtener información, consulte [Deploy Projects to Integration Services Server](../deploy-projects-to-integration-services-server.md).  
  
 Para almacenar un paquete en el almacén de paquetes SSIS, la base de datos msdb o en el sistema de archivos, utilice el modelo de implementación de paquetes. Para obtener más información, vea [implementación de paquetes &#40;SSIS&#41;](legacy-package-deployment-ssis.md).  
  
|Herramienta|Paquetes que están almacenados en el servidor de Integration Services|Paquetes que están almacenados en el almacén de paquetes SSIS o en la base de datos msdb|Paquetes que están almacenados en el sistema de archivos, fuera de la ubicación que forma parte del almacén de paquetes SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|No|No<br /><br /> Pero puede agregar un paquete existente a un proyecto del almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que incluye la base de datos msdb. La inclusión de un paquete existente en el proyecto de este modo crea una copia local del paquete en el sistema de archivos.|Sí|  
|**SQL Server Management Studio, cuando está conectado a una instancia del Motor de base de datos que hospeda el servidor de Integration Services**<br /><br /> Para obtener más información, consulte [Execute Package Dialog Box](../execute-package-dialog-box.md).|Sí|No<br /><br /> Sin embargo, puede importar un paquete al servidor desde estas ubicaciones.|No<br /><br /> Sin embargo, puede importar un paquete al servidor desde el sistema de archivos.|  
|**SQL Server Management Studio, cuando está conectado al servicio Integration Services que administra el almacén de paquetes SSIS**|No|Sí|No<br /><br /> Sin embargo, puede importar un paquete al almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] desde el sistema de archivos.|  
|**DTExec**<br /><br /> Para obtener más información, vea [DTExec Utility](dtexec-utility.md).|Sí|Sí|Sí|  
|**dtexecui**<br /><br /> Para más información, vea [Referencia de la interfaz de usuario de la Utilidad de ejecución de paquetes &#40;DtExecUI&#41;](execute-package-utility-dtexecui-ui-reference.md)|No|Sí|Sí|  
|**Agente SQL Server**<br /><br /> Use un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar un paquete.<br /><br /> Para más información, consulte [SQL Server Agent Jobs for Packages](sql-server-agent-jobs-for-packages.md).|Sí|Sí|Sí|  
|**Procedimiento almacenado integrado**<br /><br /> Para más información, vea [catalog.start_execution &#40;base de datos de SSISDB&#41;](/sql/integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database)|Sí|No|No|  
|**API administrada, mediante el uso de tipos y miembros en el** <xref:Microsoft.SqlServer.Management.IntegrationServices> espacio de nombres|Sí|No|No|  
|**API administrada, mediante el uso de tipos y miembros en el** <xref:Microsoft.SqlServer.Dts.Runtime> espacio de nombres|No actualmente|Sí|Sí|  
  
## <a name="execution-and-logging"></a>Ejecución y registro  
 Los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se pueden habilitar para el registro y el usuario puede capturar la información en tiempo de ejecución de los archivos de registro. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../performance/integration-services-ssis-logging.md).  
  
 Puede supervisar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se implementan y se ejecutan en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante informes de operación. Los informes están disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Reports for the Integration Services Server](../reports-for-the-integration-services-server.md).  
  
## <a name="related-tasks"></a>Related Tasks  
  
-   [Programar un paquete mediante el Agente SQL Server](../schedule-a-package-by-using-sql-server-agent.md)  
  
-   [Ejecutar un paquete en SQL Server Data Tools](../run-a-package-in-sql-server-data-tools.md)  
  
-   [Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio](../run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Consulte también  
 [Utilidad DTExec](dtexec-utility.md)   
 [Asistente para importación y exportación de SQL Server](../import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md)  
  
  
