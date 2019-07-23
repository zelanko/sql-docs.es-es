---
title: Herramientas y utilidades de SQL para SQL Server, Azure SQL Database y Azure SQL Data Warehouse | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
ms.assetid: ''
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: fe249e4df9c33fcbb292fc93f218e16ae111b0bb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68105659"
---
# <a name="sql-tools-and-utilities-for-sql-server-azure-sql-database-and-azure-sql-data-warehouse"></a>Herramientas y utilidades de SQL para SQL Server, Azure SQL Database y Azure SQL Data Warehouse
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Para administrar (consultar, supervisar, etc.) la base de datos, necesita una herramienta. Mientras que las bases de datos se pueden ejecutar en la nube, en Windows o en [Linux](../linux/sql-server-linux-overview.md), no es necesario que la herramienta se ejecute en la misma plataforma que la base de datos. 

Hay muchas herramientas de base de datos disponibles, por lo que en este artículo se proporcionan descripciones y punteros a algunas de las herramientas disponibles para trabajar con las bases de datos SQL. Si necesita ayuda para decidir qué herramienta necesita, consulte ¿ [qué herramienta debo usar?](#which-tool-should-i-choose).

## <a name="gui-tools-to-manage-databases"></a>Herramientas de GUI para administrar bases de datos  

A continuación se muestran las principales herramientas de la interfaz gráfica de usuario (GUI):

| Herramienta | Descripción | Se ejecuta el |
|:--|:--|:--|
| [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md) | [!INCLUDE[name-sos](../includes/name-sos-short.md)]es una herramienta gratuita y ligera para administrar bases de datos dondequiera que se estén ejecutando. Esta versión preliminar proporciona características de administración de bases de datos, incluido un editor de Transact-SQL extendido e información personalizable sobre el estado operativo de las bases de datos. | **se ejecuta en Windows, MacOS y Linux. [!INCLUDE[name-sos](../includes/name-sos-short.md)]**|
| [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md) | Use SQL Server Management Studio (SSMS) para consultar, diseñar y administrar SQL Server, Azure SQL Database y Azure SQL Data Warehouse. | **SSMS se ejecuta en Windows**.|
| [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md) | Convierta Visual Studio en un entorno de desarrollo eficaz para SQL Server, Azure SQL Database y Azure SQL Data Warehouse.| **SSDT se ejecuta en Windows**.|
| [Visual Studio Code](https://code.visualstudio.com/)| Después de instalar Visual Studio Code, instale la [extensión MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) para desarrollar Microsoft SQL Server, Azure SQL Database y SQL Data Warehouse.| **Visual Studio Code se ejecuta en Windows, MacOS y Linux**.|


## <a name="command-line-tools-to-manage-databases"></a>Herramientas de línea de comandos para administrar bases de datos

A continuación se muestran las herramientas de línea de comandos principales:

| Herramienta | Descripción | Se ejecuta el |
|:--|:--|:--|
|[**mssql-cli (preview)** ](mssql-cli.md)|**MSSQL-CLI** es una herramienta de línea de comandos interactiva para consultar SQL Server. | Windows, macOS y Linux|
| [**sqlpackage**](sqlpackage.md) |**sqlpackage** es una utilidad de línea de comandos que automatiza varias tareas de desarrollo de bases de datos. las versiones de macOS y Linux de sqlpackage se encuentran actualmente en versión preliminar. | Windows, macOS y Linux|
|[**SQL Server PowerShell**](../powershell/sql-server-powershell.md)| **SQL Server PowerShell** proporciona cmdlets para trabajar con SQL| Windows, macOS y Linux|
| [**sqlcmd**](sqlcmd-utility.md) |la utilidad **sqlcmd** permite escribir instrucciones TRANSACT-SQL, procedimientos del sistema y archivos de script en el símbolo del sistema. | Windows, macOS y Linux|
|[**bcp**](https://docs.microsoft.com/sql/tools/bcp-utility?view=sql-server-2014)|La utilidad de **p**rograma **d**e **p**copia masiva (**bcp**) hace copias masivas de los datos entre una instancia de [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y un archivo de datos en un formato especificado por el usuario.|Windows, macOS y Linux|
|[**mssql-scripter (versión preliminar)** ](https://github.com/Microsoft/mssql-scripter)|**MSSQL-scripter** es una experiencia de línea de comandos multiplataforma para la generación de scripts de bases de datos SQL Server|Windows, macOS y Linux|
|[**mssql-conf**](../linux/sql-server-linux-configure-mssql-conf.md)|**MSSQL-conf** configura SQL Server que se ejecutan en Linux.|Linux|



## <a name="which-tool-should-i-choose"></a>¿Qué herramienta debo elegir?

- ¿Desea administrar una instancia de SQL Server o una base de datos, en un editor ligero en Windows, Linux o Mac? Seleccionar [[!INCLUDE[name-sos](../includes/name-sos.md)]](../sql-operations-studio/download.md)
- ¿Desea administrar una instancia de SQL Server o una base de datos en Windows con compatibilidad completa con GUI? Seleccionar [SQL Server Management Studio (SSMS)](../ssms/download-sql-server-management-studio-ssms.md)
- ¿Desea crear o mantener código de base de datos, incluida la validación en tiempo de compilación, la refactorización y la compatibilidad con el diseñador en Windows? Seleccionar [SQL Server Data Tools (SSDT)](../ssdt/download-sql-server-data-tools-ssdt.md)
- ¿Desea consultar SQL Server con una herramienta de línea de comandos que incluye IntelliSense, la alta iluminación de la sintaxis, etc.? Elija [mssql-cli](mssql-cli.md).
- ¿Desea escribir scripts de T-SQL en un editor ligero en Windows, Linux o Mac? Elegir [Visual Studio Code](https://code.visualstudio.com/) y la [extensión MSSQL](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)



## <a name="additional-tools"></a>Herramientas adicionales

| Herramienta | Descripción |
|:--|:--|
| [Administrador de configuración](../tools/configuration-manager/sql-server-configuration-manager-help.md) | Use Administrador de configuración de SQL Server para configurar SQL Server Services y configurar la conectividad de red. Configuration Manager se ejecuta en Windows|
| [SQL Server Migration Assistant](../ssma/sql-server-migration-assistant.md) | Use Microsoft SQL Server Migration Assistant para automatizar la migración de bases de datos a SQL Server desde Microsoft Access, DB2, MySQL, Oracle y Sybase.|
| [Asistente para experimentación con base de datos](../dea/database-experimentation-assistant-overview.md) | Use Asistente para experimentación con bases de datos para evaluar una versión de destino de SQL para una carga de trabajo determinada. |
| [Distributed Replay](../tools/distributed-replay/install-distributed-replay-overview.md) | Use la característica Distributed Replay para ayudarle a evaluar el impacto de las futuras actualizaciones de SQL Server. Utilice también Distributed Replay para ayudar a evaluar el impacto de las actualizaciones del hardware y del sistema operativo, y la optimización de SQL Server. |
| [ssbdiagnose](../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md) | La utilidad ssbdiagnose notifica problemas en las conversaciones Service Broker o la configuración de Service Broker Services. |

Si está buscando herramientas adicionales que no se mencionan en esta página, consulte [utilidades del símbolo del sistema de SQL](command-prompt-utility-reference-database-engine.md).

