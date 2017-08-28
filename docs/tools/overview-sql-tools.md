---
title: Herramientas SQL y las utilidades de SQL Server, base de datos SQL Azure y almacenamiento de datos SQL | Documentos de Microsoft
ms.custom: 
ms.date: 08/25/2017
ms.prod: sql-server-2017
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 
caps.latest.revision: 0
author: stevestein
ms.author: sstein
manager: craigg
ms.translationtype: MT
ms.sourcegitcommit: 21f0cfd102a6fcc44dfc9151750f1b3c936aa053
ms.openlocfilehash: eccbe54c561e009858f6192126abc57e3399082c
ms.contentlocale: es-es
ms.lasthandoff: 08/28/2017

---
# <a name="tools-and-utilities-for-azure-sql-database-sql-server-and-sql-data-warehouse"></a>Herramientas y utilidades de base de datos de SQL Azure, SQL Server y almacenamiento de datos de SQL

[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]  

![](../includes/media/sql-database-tools.png)Este artículo proporciona una lista de herramientas disponibles para trabajar con SQL Server, base de datos de SQL Azure, almacenamiento de datos SQL y las aplicaciones basadas en SQL Server. 

Si desea saltar directamente en y empezar a crear tablas, ejecutar consultas, básicamente diseñar y administrar la base de datos, a continuación, [ **SQL Server Management Studio (SSMS)** ](../ssms/download-sql-server-management-studio-ssms.md) es muy probable que la herramienta preferida. SSMS es gratuita y se ejecuta en Windows.

Si estás ejecutando Linux o Mac OS, intente [código de Visual Studio](https://code.visualstudio.com/) con el [ **mssql para el código de Visual Studio** ](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) extensión. Estas herramientas son para el desarrollo de Microsoft SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL con un amplio conjunto de funcionalidades y también son gratuitas. Vea [usar código de Visual Studio para crear y ejecutar secuencias de comandos de Transact-SQL para SQL Server](../linux/sql-server-linux-develop-use-vscode.md).


## <a name="sql-tools"></a>Herramientas SQL 
 
| Herramienta | Description |
|:--|:--|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Usar SQL Server Management Studio (SSMS) para consultar, diseñar y administrar el almacenamiento de datos de SQL Azure, SQL Server y base de datos de SQL Azure. |
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Convertir Visual Studio en un entorno de desarrollo eficaz para SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL Azure. |
| [Código de Visual Studio](https://code.visualstudio.com/)| Código de Visual Studio funciona en Linux, Mac OS y Windows. Después de instalar Visual Studio Code, instalar el [mssql extensión](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para el desarrollo de Microsoft SQL Server, base de datos de SQL Azure y almacenamiento de datos de SQL. |
| [Administrador de configuración](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Utilice el Administrador de configuración de SQL Server para configurar servicios de SQL Server y configurar la conectividad de red.|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Usar SQL Server Migration Assistant para automatizar la migración de base de datos a SQL Server desde Microsoft Access, DB2, MySQL, Oracle y Sybase.|
| [Reproducción distribuida](../tools/distributed-replay/install-distributed-replay-overview.md) | Utilice la característica Distributed Replay para ayudarle a evaluar el impacto de las actualizaciones futuras de SQL Server. Usar Distributed Replay para ayudar a evaluar el impacto de hardware y actualizaciones del sistema operativo y SQL Server para la optimización. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | La utilidad ssbdiagnose informa de problemas en las conversaciones de Service Broker o la configuración de servicios de Service Broker. |


## <a name="sql-command-prompt-utilities"></a>Utilidades del símbolo del sistema de SQL

  Las utilidades de símbolo del sistema permiten incluir en scripts las operaciones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . La siguiente tabla contiene una lista de utilidades de símbolo del sistema que se suministran junto con [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
|**Utilidad**|**Descripción**|**Instalada en**|  
|-----------------|---------------------|----------------------|  
|[bcp (utilidad)](../tools/bcp-utility.md)|Se usa para copiar datos entre una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y un archivo de datos en un formato especificado por el usuario.|\<*unidad*: > \Program Files\\[!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]\Client SDK\ODBC\110\Tools\Binn|  
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

## <a name="sql-command-prompt-utilities-syntax-conventions"></a>Convenciones de sintaxis de utilidades de símbolo del sistema de SQL  
  
|**Convención**|**Se usa para**|  
|--------------------|------------------|  
|UPPERCASE|Instrucciones y términos usados en el sistema operativo.|  
|`monospace`|Comandos y código de programación de ejemplo.|  
|*cursiva*|Parámetros proporcionados por el usuario.|  
|**Negrita**|Comandos, parámetros y otros elementos de sintaxis que deben escribirse exactamente como se muestran.|  



