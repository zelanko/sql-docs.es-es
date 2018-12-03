---
title: Herramientas SQL y utilidades para SQL Server, base de datos SQL Azure y Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 84cebceddc18ee3d288226ebd00bc86ea25ac926
ms.sourcegitcommit: eb1f3a2f5bc296f74545f17d20c6075003aa4c42
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2018
ms.locfileid: "52190995"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>Herramientas SQL y utilidades para SQL Server, base de datos SQL Azure y Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para administrar (consulta, monitor, etc.) necesitan una herramienta de la base de datos. Mientras que las bases de datos pueden ejecutarse en la nube, en Windows o en [Linux](../linux/sql-server-linux-overview.md), la herramienta no tiene que ejecutarse en la misma plataforma que la base de datos. 

Hay muchas herramientas de base de datos disponibles, por lo que en este artículo se ofrece las descripciones y punteros a algunas de las herramientas disponibles para trabajar con las bases de datos SQL. Si necesita ayuda para decidir qué herramienta necesita, consulte [qué herramienta debo usar?](#which-tool-should-i-choose).


## <a name="gui-tools-to-manage-databases"></a>Herramientas de GUI para administrar las bases de datos  

Estas son las herramientas de (GUI) de la interfaz gráfica de usuario principal:

| Herramienta | Descripción | Se ejecuta en |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)] es una herramienta gratuita y ligera, para administrar las bases de datos siempre que se están ejecutando. Esta versión preliminar proporciona características de administración de base de datos, incluido un editor de Transact-SQL extendido y personalizables información sobre el estado operativo de las bases de datos. | **[!INCLUDE[name-sos](../includes/name-sos-short.md)] se ejecuta en Windows, macOS y Linux**.|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Use SQL Server Management Studio (SSMS) para consultar, diseñar y administrar SQL Server, Azure SQL Database y Azure SQL Data Warehouse. | **SSMS se ejecuta en Windows**.|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Convierta Visual Studio en un entorno de desarrollo eficaz para SQL Server, Azure SQL Database y Azure SQL Data Warehouse.| **SSDT se ejecuta en Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Después de instalar Visual Studio Code, instale el [extensión mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para el desarrollo de Microsoft SQL Server, Azure SQL Database y SQL Data Warehouse.| **Código de Visual Studio se ejecuta en Windows, macOS y Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Herramientas de línea de comandos para administrar las bases de datos

Los siguientes son las principales herramientas de línea de comandos:

| Herramienta | Descripción | Se ejecuta en |
|:--|:--|:--|
|[**mssql-cli (preview)**](mssql-cli.md)|**MSSQL-cli** es una herramienta de línea de comandos interactiva para realizar consultas en SQL Server. | Windows, macOS y Linux|
| [**sqlpackage**](sqlpackage.md) |**Sqlpackage** es una utilidad de línea de comandos que automatiza varias tareas de desarrollo de base de datos. macOS y Linux versiones de sqlpackage están actualmente en versión preliminar. | Windows, macOS y Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** proporciona cmdlets para trabajar con SQL| Windows, macOS y Linux|
| [**sqlcmd**](sqlcmd-utility.md) |**Sqlcmd** utilidad le permite escribir instrucciones Transact-SQL, procedimientos del sistema y archivos de script en el símbolo del sistema. | Windows, macOS y Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|La utilidad de **p**rograma **d**e **p**copia masiva (**bcp**) hace copias masivas de los datos entre una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y un archivo de datos en un formato especificado por el usuario.|Windows, macOS y Linux|
|[**MSSQL-generador de scripts (versión preliminar)**](https://github.com/Microsoft/mssql-scripter)|**MSSQL scripter** es una experiencia de línea de comandos multiplataforma para secuencias de comandos de las bases de datos de SQL Server|Windows, macOS y Linux|
|[**MSSQL-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura SQL Server que se ejecutan en Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>¿Qué herramienta debo elegir?

- ¿Desea administrar una instancia de SQL Server o la base de datos, en un editor ligero en Windows, Linux o Mac? Seleccionar [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- ¿Desea administrar una instancia de SQL Server o la base de datos en Windows con compatibilidad total con la interfaz gráfica de usuario? Seleccionar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- ¿Desea crear o mantener el código de la base de datos, incluida la validación en tiempo de compilación, refactorización y el diseñador se admiten en Windows? Seleccionar [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- ¿Si desea consultar SQL Server con una herramienta de línea de comandos que incluye IntelliSense, sintaxis alto-iluminación, y mucho más? Elija [mssql-cli](mssql-cli.md)
- ¿Desea escribir secuencias de comandos de T-SQL en un editor ligero en Windows, Linux o Mac? Elija [Visual Studio Code](https://code.visualstudio.com/) y [extensión mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Herramientas adicionales

| Herramienta | Descripción |
|:--|:--|
| [Administrador de configuración](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use el Administrador de configuración de SQL Server para configurar servicios de SQL Server y configurar la conectividad de red. Configuration Manager se ejecuta en Windows|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Use Microsoft SQL Server Migration Assistant para automatizar la migración de bases de datos a SQL Server desde Microsoft Access, DB2, MySQL, Oracle y Sybase.|
| [Asistente para experimentación con base de datos](../dea/database-experimentation-assistant-overview.md) | Use el Asistente de experimentación de base de datos para evaluar una versión de destino de SQL para una carga de trabajo. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use la característica Distributed Replay para ayudarle a evaluar el impacto de las actualizaciones futuras de SQL Server. También puede usar Distributed Replay para ayudar a evaluar el impacto de hardware y actualizaciones del sistema operativo y la optimización de SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | La utilidad ssbdiagnose informa de problemas en las conversaciones de Service Broker o la configuración de servicios de Service Broker. |

Si está buscando herramientas adicionales que no se mencionan en esta página, consulte [utilidades de línea de comandos SQL](command-prompt-utility-reference-database-engine.md).

