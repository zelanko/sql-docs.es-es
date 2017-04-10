---
title: "Ejecutar paquetes de Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "12/16/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Paquetes de Integration Services, ejecutar"
  - "paquetes SSIS, ejecutar"
  - "paquetes [Integration Services], ejecución"
  - "paquetes de SQL Server Integration Services, ejecutar"
  - "ejecutar paquetes [Integration Services]"
  - "ejecutar paquetes [Integration Services]"
  - "Integration Services, (vea también paquetes de Integration Services)"
ms.assetid: c5fecc23-6f04-4fb2-9a29-01492ea41404
caps.latest.revision: 65
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 61
---
# Ejecutar paquetes de Integration Services (SSIS)
  Para ejecutar un paquete de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , puede utilizar una de las herramientas en función de dónde se almacenan los paquetes. Las herramientas se enumeran en la tabla a continuación.  
  
 Para almacenar un paquete en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , utilice el modelo de implementación del proyecto para implementar el proyecto en el servidor. Para obtener información, consulte [Deploy Projects to Integration Services Server](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
 Para almacenar un paquete en el almacén de paquetes SSIS, la base de datos msdb o en el sistema de archivos, utilice el modelo de implementación de paquetes. Para más información, vea [Implementación de paquetes heredada &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
|Herramienta|Paquetes que están almacenados en el servidor de Integration Services|Paquetes que están almacenados en el almacén de paquetes SSIS o en la base de datos msdb|Paquetes que están almacenados en el sistema de archivos, fuera de la ubicación que forma parte del almacén de paquetes SSIS|  
|----------|-----------------------------------------------------------------|--------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------|  
|**SQL Server Data Tools**|No|No<br /><br /> Pero puede agregar un paquete existente a un proyecto del almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] , que incluye la base de datos msdb. La inclusión de un paquete existente en el proyecto de este modo crea una copia local del paquete en el sistema de archivos.|Sí|  
|**SQL Server Management Studio, cuando está conectado a una instancia del motor de base de datos que hospeda el servidor de Integration Services**<br /><br /> Para obtener más información, consulte [Execute Package Dialog Box](../../integration-services/packages/execute-package-dialog-box.md).|Sí|No<br /><br /> Sin embargo, puede importar un paquete al servidor desde estas ubicaciones.|No<br /><br /> Sin embargo, puede importar un paquete al servidor desde el sistema de archivos.|
|**SQL Server Management Studio, cuando está conectado a una instancia del motor de base de datos que hospeda el servidor de Integration Services que está habilitado como patrón de escalado horizontal**<br /><br /> Para obtener más información, consulte [Ejecutar paquetes en el escalado horizontal](../../integration-services/run-packages-in-integration-services-ssis-scale-out.md).|Sí|No|No|
|**SQL Server Management Studio, cuando está conectado al servicio Integration Services que administra el almacén de paquetes SSIS**|No|Sí|No<br /><br /> Sin embargo, puede importar un paquete al almacén de paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] desde el sistema de archivos.|  
|**dtexec**<br /><br /> Para más información, consulte [dtexec Utility](../../integration-services/packages/dtexec-utility.md).|Sí|Sí|Sí|  
|**dtexecui**<br /><br /> Para más información, vea [Referencia de la interfaz de usuario de la Utilidad de ejecución de paquetes &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md)|No|Sí|Sí|  
|**Agente SQL Server**<br /><br /> Use un trabajo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para programar un paquete.<br /><br /> Para más información, consulte [SQL Server Agent Jobs for Packages](../../integration-services/packages/sql-server-agent-jobs-for-packages.md).|Sí|Sí|Sí|  
|**Procedimiento almacenado integrado**<br /><br /> Para más información, vea [catalog.start_execution &#40;base de datos de SSISDB&#41;](../../integration-services/system-stored-procedures/catalog-start-execution-ssisdb-database.md)|Sí|No|No|  
|**API administrada, usando tipos y miembros en el** <xref:Microsoft.SqlServer.Management.IntegrationServices> |Sí|No|No|  
|**API administrada, usando tipos y miembros en el** <xref:Microsoft.SqlServer.Dts.Runtime> |No actualmente|Sí|Sí|  
  
## <a name="execution-and-logging"></a>Ejecución y registro  
 Los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] se pueden habilitar para el registro y el usuario puede capturar la información en tiempo de ejecución de los archivos de registro. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
 Puede supervisar los paquetes de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que se implementan y se ejecutan en el servidor [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] mediante informes de operación. Los informes están disponibles en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Para obtener más información, consulte [Reports for the Integration Services Server](../../integration-services/performance/reports-for-the-integration-services-server.md).  
  
## <a name="related-tasks"></a>Tareas relacionadas  
  
-   [Programar un paquete mediante el Agente SQL Server](../../integration-services/packages/schedule-a-package-by-using-sql-server-agent.md)  
  
-   [Ejecutar un paquete en SQL Server Data Tools](../../integration-services/packages/run-a-package-in-sql-server-data-tools.md)  
  
-   [Ejecutar un paquete en el servidor SSIS con SQL Server Management Studio](../../integration-services/packages/run-a-package-on-the-ssis-server-using-sql-server-management-studio.md)  
  
## <a name="see-also"></a>Vea también  
 [dtexec (utilidad)](../../integration-services/packages/dtexec-utility.md)   
[Start the SQL Server Import and Export Wizard](../../integration-services/import-export-data/start-the-sql-server-import-and-export-wizard.md) (Iniciar el Asistente para importación y exportación de SQL Server)
  
  