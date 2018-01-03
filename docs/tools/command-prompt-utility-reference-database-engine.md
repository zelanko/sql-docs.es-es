---
title: "Utilidades de símbolo del sistema de SQL (motor de base de datos) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: misc
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- command prompt utilities [SQL Server]
- command prompt utilities [SQL Server], about command prompt utilities
- command prompt [SQL Server]
- utilities [SQL Server], command prompt
- command prompt [SQL Server], utilities
ms.assetid: 48364bd9-6ea7-45e9-a332-acf3d81bbfae
caps.latest.revision: "90"
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 9939c015b3c163d8de8b70c626c0b9108a48269c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sql-command-prompt-utilities-database-engine"></a>Utilidades de símbolo del sistema de SQL (motor de base de datos)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]Utilidades de símbolo del sistema permiten incluir en scripts [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] operaciones. La siguiente tabla contiene una lista de utilidades de símbolo del sistema que se suministran junto con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|**Utilidad**|**Descripción**|**Instalada en**|  
|-----------------|---------------------|----------------------|  
|[bcp (utilidad)](../tools/bcp-utility.md)|Usar para copiar datos entre una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y un archivo de datos en un formato especificado por el usuario.|\<*unidad*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[dta (utilidad)](../tools/dta/dta-utility.md)|Se utiliza para analizar una carga de trabajo y recomendar estructuras de diseño físico para optimizar el rendimiento del servidor para esa carga de trabajo.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[dtexec (utilidad)](../integration-services/packages/dtexec-utility.md)|Se usa para configurar y ejecutar un paquete de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Una versión de interfaz de usuario de esta utilidad del símbolo del sistema se denomina **DTExecUI**y abre la utilidad de ejecución de paquetes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[dtutil (utilidad)](../integration-services/dtutil-utility.md)|Se usa para administrar paquetes SSIS.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]DTS\Binn|  
|[Implementar soluciones de modelos con la utilidad de implementación](../analysis-services/multidimensional-models/deploy-model-solutions-with-the-deployment-utility.md)|Se utiliza para implementar proyectos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en instancias de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VShell\Common7\IDE|  
|[MSSQL-scripter (vista previa pública)](https://blogs.technet.microsoft.com/dataplatforminsider/2017/05/17/try-new-sql-server-command-line-tools-to-generate-t-sql-scripts-and-monitor-dynamic-management-views/)|Se usa para generar scripts de crear e insertar T-SQL para objetos de base de datos de SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL Azure.|Consulte nuestro [repositorio de GitHub](https://github.com/Microsoft/sql-xplat-cli) para obtener información de descarga y uso.| 
|[osql (utilidad)](../tools/osql-utility.md)|Permite especificar instrucciones, procedimientos del sistema y archivos de scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] en el símbolo del sistema.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Analizador (utilidad)](../tools/profiler-utility.md)|Se utiliza para iniciar [!INCLUDE[ssSqlProfiler](../includes/sssqlprofiler-md.md)] desde un símbolo del sistema.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[Utilidad RS.exe &#40;SSRS&#41;](../reporting-services/tools/rs-exe-utility-ssrs.md)|Se utiliza para ejecutar scripts diseñados para administrar servidores de informes de [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rsconfig (utilidad) &#40;SSRS&#41;](../reporting-services/tools/rsconfig-utility-ssrs.md)|Se utiliza para configurar una conexión de servidor de informes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[rskeymgmt (utilidad) &#40;SSRS&#41;](../reporting-services/tools/rskeymgmt-utility-ssrs.md)|Se utiliza para administrar claves de cifrado en un servidor de informes.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlagent90 (aplicación)](../tools/sqlagent90-application.md)|Se usa para iniciar el Agente de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] desde un símbolo del sistema.|\<unidad >: \Program SQL Server\\<*instance_name*> \MSSQL\Binn|  
|[sqlcmd Utility](../tools/sqlcmd-utility.md)|Permite especificar instrucciones, procedimientos del sistema y archivos de scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] en el símbolo del sistema.|\<*unidad*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
|[SQLdiag (utilidad)](../tools/sqldiag-utility.md)|Se usa para recopilar información de diagnóstico para el Servicio de soporte y atención al cliente de [!INCLUDE[msCoName](../includes/msconame-md.md)] .|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqllogship (aplicación)](../tools/sqllogship-application.md)|Las aplicaciones lo utilizan para realizar operaciones de copia de seguridad, copia y restauración, y tareas de limpieza asociadas en una configuración de trasvase de registros sin ejecutar trabajos de copia de seguridad, copia y restauración.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[SqlLocalDB (utilidad)](../tools/sqllocaldb-utility.md)|Un modo de ejecución de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] destinado a los desarrolladores de programas.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\|  
|[sqlmaint (utilidad)](../tools/sqlmaint-utility.md)|Se usa para ejecutar los planes de mantenimiento de bases de datos creados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].|\<unidad >: \Program SQL Server\MSSQL13. MSSQLSERVER\MSSQL\Binn|  
|[Utilidad sqlps](../tools/sqlps-utility.md)|Se usa para ejecutar comandos y scripts de PowerShell. Carga y registra el proveedor de PowerShell de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y los cmdlets.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn|  
|[sqlservr](../tools/sqlservr-application.md)|Se usa para iniciar y detener una instancia de [!INCLUDE[ssDE](../includes/ssde-md.md)] desde el símbolo del sistema para solucionar problemas.|\<unidad >: \Program SQL Server\MSSQL13. MSSQLSERVER\MSSQL\Binn|  
|[Ssms (Utilidad)](../tools/sql-server-management-studio/ssms-utility.md)|Se utiliza para iniciar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] desde un símbolo del sistema.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]Tools\Binn\VSShell\Common7\IDE|  
|[tablediff (utilidad)](../tools/tablediff-utility.md)|Se utiliza para comparar los datos de dos tablas y ver si no convergen, lo que es útil para solucionar problemas de una topología de replicación.|[!INCLUDE[ssInstallPathVar](../includes/ssinstallpathvar-md.md)]COM|  

## <a name="command-prompt-utilities-syntax-conventions"></a>Convenciones de la sintaxis de las herramientas del símbolo del sistema  
  
|**Convención**|**Se usa para**|  
|--------------------|------------------|  
|UPPERCASE|Instrucciones y términos usados en el sistema operativo.|  
|`monospace`|Comandos y código de programación de ejemplo.|  
|*cursiva*|Parámetros proporcionados por el usuario.|  
|**Negrita**|Comandos, parámetros y otros elementos de sintaxis que deben escribirse exactamente como se muestran.|  
  
## <a name="see-also"></a>Vea también  
 [Agente de distribución de replicación](../relational-databases/replication/agents/replication-distribution-agent.md)   
 [Agente de registro del LOG de replicación](../relational-databases/replication/agents/replication-log-reader-agent.md)   
 [Agente de mezcla de replicación](../relational-databases/replication/agents/replication-merge-agent.md)   
 [Agente de lectura de cola de replicación](../relational-databases/replication/agents/replication-queue-reader-agent.md)   
 [Replication Snapshot Agent](../relational-databases/replication/agents/replication-snapshot-agent.md)  
  
  
