---
title: Preguntas más frecuentes sobre Azure Data Studio
description: Obtenga respuestas a preguntas frecuentes sobre Azure Data Studio, como "¿Qué hace?", "¿Quién debería usarlo?" y "¿Cuánto cuesta?".
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: alayu, maghan
ms.custom: seodec18
ms.date: 10/20/2020
ms.openlocfilehash: 0e32a9e0a9e7dfd14c56c31a065f692c535b24fb
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257355"
---
# <a name="azure-data-studio-faq"></a>Preguntas más frecuentes sobre Azure Data Studio

## <a name="what-is-azure-data-studio"></a>¿Qué es Azure Data Studio?

Azure Data Studio es un entorno de escritorio multiplataforma de código abierto para profesionales de datos que usan la familia de las plataformas de datos locales y en la nube de Azure Data en Windows, macOS y Linux. Azure Data Studio, que anteriormente se había publicado con el nombre de versión preliminar SQL Operations Studio, ofrece una experiencia de editor moderna con IntelliSense rápido y ligero, fragmentos de código, integración del control de código fuente y un terminal integrado. Se ha diseñado con el usuario de la plataforma de datos en mente, con gráficos integrados de conjuntos de resultados de consultas y paneles personalizables.

La investigación ha demostrado que los usuarios pasan mucho más tiempo trabajando en la edición de consultas que en cualquier otra tarea con SQL Server Management Studio. Por ese motivo, Azure Data Studio se ha diseñado para centrarse profundamente en la funcionalidad más usada, con experiencias adicionales disponibles como extensiones opcionales en el producto. Esto permite a todos los usuarios personalizar su entorno a los flujos de trabajo que usan con mayor frecuencia.

## <a name="how-much-does-azure-data-studio-cost"></a>¿Cuánto cuesta Azure Data Studio?

Azure Data Studio es gratuito para el uso comercial o privado.

## <a name="who-should-use-azure-data-studio"></a>¿Quién debería usar Azure Data Studio?

Cualquier persona puede usar Azure Data Studio. Con todo, se ha diseñado para simplificar las tareas que realizan los desarrolladores de bases de datos, los administradores de bases de datos, los administradores del sistema y los proveedores de software independientes.

## <a name="what-can-i-do-with-azure-data-studio"></a>¿Qué puedo hacer con Azure Data Studio?

Azure Data Studio se basa en Visual Studio Code y ofrece una experiencia ligera de flujo de trabajo de código moderno centrada en el teclado al trabajar con SQL Server, Azure SQL Database y Azure Synapse Analytics. Azure Data Studio hace que las experiencias principales en las que se basa a diario sean sencillas y fáciles con características integradas como varias ventanas de pestañas, un editor de SQL completo, IntelliSense, finalización de palabras clave, navegación de código y fragmentos de código, e integración del control de código fuente (GIT y TFS). Puede ejecutar consultas a petición, ver y guardar resultados como texto, JSON o Excel, editar datos, organizar y administrar sus conexiones de bases de datos favoritas y examinar objetos de base de datos en una experiencia de exploración de objetos que ya conoce.

Use sus herramientas de línea de comandos favoritas (por ejemplo, Bash, PowerShell, sqlcmd, bcp, psql y ssh) en la ventana del terminal integrado directamente desde la interfaz de usuario de Azure Data Studio. Genere y ejecute fácilmente los scripts CREATE e INSERT para los objetos de base de datos con el fin de crear copias de la base de datos con fines de desarrollo o prueba. Aumente su productividad con fragmentos de código inteligentes y experiencias gráficas completas que crean nuevas bases de datos y objetos de base de datos (como tablas, vistas, procedimientos almacenados, usuarios, inicios de sesión, roles, etc.) o actualizan los objetos de base de datos existentes. Use paneles personalizables completos para supervisar y solucionar rápidamente los cuellos de botella de rendimiento en las bases de datos locales, en Azure o en cualquier nube.

Azure Data Studio ofrece una experiencia coherente para realizar copias de seguridad de las bases de datos y restaurarlas. Con compatibilidad planeada con los grupos de disponibilidad Always On de SQL Server, puede configurar, supervisar y solucionar problemas fácilmente de los grupos de disponibilidad para las bases de datos de SQL Server críticas y conmutar por error rápidamente a una base de datos secundaria durante un desastre. Azure Data Studio se ha diseñado para que sea más productivo en el ciclo de vida de DevOps de las bases de datos que elija en los sistemas operativos que quiera. Como consecuencia, siempre tiene el control y puede reducir los riesgos, resolver los problemas más rápido y ofrecer continuamente un valor que supere las expectativas de los clientes.

## <a name="is-azure-data-studio-open-source"></a>¿Azure Data Studio es de código abierto?

El código fuente de Azure Data Studio y sus proveedores de datos está disponible en GitHub. El código fuente del servidor front-end de [Azure Data Studio](https://github.com/microsoft/azuredatastudio) (que se basa en Visual Studio Code) está disponible en los términos de licencia del código fuente que proporcionan derechos para modificar y usar el software, pero no para redistribuirlo ni hospedarlo en un servicio en la nube. El código fuente de los proveedores de datos está disponible bajo la licencia MIT en [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>¿Tenemos previsto que SSMS sea de código abierto?

No. Pero las herramientas de la GUI y la CLI de varios sistemas operativos de la próxima generación son de código abierto. Por ejemplo, la extensión de mssql para VS Code, mssql-scripter y msql-CLI son de código abierto en GitHub. El código fuente de Azure Data Studio está disponible en GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>Ahora que existe Azure Data Studio, ¿Microsoft tiene previsto dejar SSMS y SSDT en desuso? 

No. Las inversiones en las herramientas insignia de Windows (SSMS, SSDT y PowerShell) continuarán además de la próxima generación de herramientas de la GUI y la CLI de varias bases de datos y varios sistemas operativos. El objetivo es ofrecer a los clientes la opción de usar las herramientas que quieran en las plataformas que elijan para sus escenarios. Azure Data Studio se centra más en las experiencias relacionadas con la edición de consultas y el desarrollo de datos, ya que la investigación ha mostrado que es la capacidad más usada en SQL Server Management Studio por una gran mayoría. También están disponibles como extensiones en Azure Data Studio otras características administrativas adicionales de alto valor, como la copia de seguridad, la restauración, la administración de trabajos del agente y la generación de perfiles de servidor. Azure Data Studio también es multiplataforma, lo que permite a los usuarios trabajar en la plataforma que quieran. En cambio, SQL Server Management Studio sigue ofreciendo la gama más amplia de funciones administrativas y sigue siendo la herramienta insignia de las tareas de administración de la plataforma. 

## <a name="when-should-i-use-azure-data-studio-or-sql-server-management-studio"></a>¿Cuándo debería usar Azure Data Studio en comparación con SQL Server Management Studio?

*Use Azure Data Studio si:*

- Está principalmente editando o ejecutando consultas.
- Necesita la capacidad de crear gráficos rápidamente y visualizar los conjuntos de resultados.
- Puede ejecutar la mayoría de las tareas administrativas mediante el terminal integrado con sqlcmd o PowerShell.
- Tiene una necesidad mínima de las experiencias del asistente.
- No necesita realizar una configuración administrativa profunda ni relacionada con la plataforma.
- Necesita ejecutarlo en macOS o Linux.

*Use SQL Server Management Studio si:*

- Lleva a cabo una configuración de la plataforma o administrativa compleja.
- Administra la seguridad, incluida la administración de usuarios, la evaluación de vulnerabilidades y la configuración de características de seguridad.
- Necesita usar los paneles y los asesores de optimización del rendimiento.
- Usa diagramas de bases de datos y diseñadores de tablas.
- Necesita acceder a los servidores registrados.
- Usa las estadísticas de consultas dinámicas o las estadísticas de cliente.

## <a name="feature-comparison"></a>Comparación de características

### <a name="shell-features"></a>Características del shell

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Inicio de sesión de Azure|Sí|Sí|
|Panel|Sí| |
|Extensiones|Sí| |
|Terminal integrado|Sí||
|Explorador de objetos|Sí|Sí|
|Scripting de objetos|Sí|Sí|
|Sistema de proyectos|Sí||
|Seleccionar elementos de la tabla|Sí|Sí|
|Control de código fuente|Sí||
|Panel de tareas|Sí||
|Temas, incluido el modo oscuro|Sí||
|Azure Resource Explorer|Versión preliminar||
|Asistente para generar scripts||Sí|
|Propiedades de objeto||Sí|
|Diseñador de tablas||Sí|

### <a name="query-editor"></a>Editor de consultas

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Visor de gráficos|Sí||
|Exportar resultados a CSV, JSON o XLSX|Sí||
|Resultados a archivo||Sí|
|Resultados a texto||Sí|
|IntelliSense|Sí|Sí|
|Fragmentos de código|Sí|Sí|
|Mostrar plan|Versión preliminar|Sí|
|Estadísticas de clientes||Sí|
|Estadísticas de consultas dinámicas||Sí|
|Opciones de consulta||Sí|
|Visor espacial||Sí|
|SQLCMD|Sí|Sí|

### <a name="operating-system-support"></a>Sistemas operativos admitidos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Sí|Sí|
|macOS|Sí||
|Linux|Sí||

### <a name="data-engineering"></a>Ingeniería de datos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Asistente de datos externos|Versión preliminar||
|Integración de HDFS|Versión preliminar||
|Cuaderno|Versión preliminar||

### <a name="database-administration"></a>Administración de bases de datos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Copia de seguridad o restauración|Sí|Sí|
|Importación de archivos planos|Sí|Sí|
|Agente SQL|Versión preliminar|Sí|
|SQL Profiler|Versión preliminar|Sí|
|Always On||Sí|
|Always Encrypted||Sí|
|Asistente para copiar datos||Sí|
|Asistente para la optimización de datos||Sí|
|Diagramas de base de datos||Sí|
|Visor de registros de errores||Sí|
|Planes de mantenimiento||Sí|
|Consulta multiservidor||Sí|
|Administración basada en directivas||Sí|
|PolyBase||Sí|
|Almacén de consultas||Sí|
|Servidores registrados||Sí|
|Replicación||Sí|
|Administración de seguridad||Sí|
|Service Broker||Sí|
|Evaluación de SQL|Versión preliminar|Sí|
|SQL Mail||Sí|
|Template Explorer||Sí|
|Evaluación de vulnerabilidad||Sí|
|Administración de XEvent||Sí|

### <a name="database-development"></a>Desarrollo de bases de datos
|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Importación o exportación de DACPAC|Sí|Sí|
|Proyectos de SQL|Versión preliminar||
|Comparación de esquemas|Sí||



## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>En Azure Data Studio falta una característica que está en SSMS o SSDT. ¿La agregarán?

Depende del escenario y la necesidad de los clientes o las empresas. Para ayudar a establecer prioridades, envíe una sugerencia y vote sobre lo existente en [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Entiendo que Azure Data Studio y la extensión de mssql para VS Code cuentan con la tecnología de un nuevo servicio de herramientas que usa las API de SMO en segundo plano. ¿SMO está disponible en Linux y macOS?

Las API de SMO aún no están disponibles en Linux ni en macOS para su consumo. Hemos migrado un subconjunto de las API de SMO a .NET Core que necesitábamos para Azure Data Studio y tenemos previsto expandirlo como parte de la hoja de ruta. SQL Tools Service está en GitHub: [https://github.com/Microsoft/sqltoolsservice](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>¿Tienen previsto trasladar las API de DACFx, sqlpackage.exe o SSDT a Linux y macOS?

Algunas partes se han completado.  [SqlPackage.exe](../tools/sqlpackage-download.md) ahora está disponible en .NET Core para Windows, macOS y Linux.  La funcionalidad de proyectos de SQL (SSDT) está habilitada en Azure Data Studio, en la [extensión SQL Database Projects](extensions/sql-database-project-extension.md).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>¿Los cmdlets de SQL PowerShell estarán disponibles en Linux y macOS?

SQL PowerShell está disponible actualmente en la galería de PowerShell y puede usarlo en Windows para trabajar con SQL Server en ejecución en cualquier lugar, incluido SQL en Linux. La oferta de los cmdlets de SQL PowerShell en Linux y macOS está en la hoja de ruta. Para ayudar a priorizarla, envíe una sugerencia en [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>¿Quién suele usar Azure Data Studio?

Los desarrolladores y DBA suelen ser los usuarios de Azure Data Studio.

## <a name="does-azure-data-studio-integrate-with-azure-synapse-analytics"></a>¿Azure Data Studio se integra con Azure Synapse Analytics?

Sí. La compatibilidad de Azure Data Studio con Azure Synapse Analytics se encuentra actualmente en versión preliminar, al igual que Azure SQL Managed Instance y los macrodatos de SQL Server 2019.

## <a name="why-is-azure-data-studio-important-for-big-data-scenarios"></a>¿Por qué es Azure Data Studio importante en escenarios de macrodatos?

Conforme SQL Server amplía sus capacidades en el espacio de los macrodatos, necesita nuevas herramientas para admitir esos casos de uso. Por ese motivo, Azure Data Studio ha publicado una nueva experiencia para los macrodatos de SQL Server, incluida la primera experiencia de cuaderno en el conjunto de herramientas de SQL Server y un nuevo Asistente para crear tablas externas que permite acceder fácil y rápidamente a los datos desde instancias remotas de SQL Server y Oracle.
