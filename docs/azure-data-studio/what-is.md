---
title: ¿Qué es Azure Data Studio
titleSuffix: Azure Data Studio
description: Azure Data Studio es una herramienta gratuita y ligera, que se ejecuta en Windows, macOS y Linux, para la administración de SQL Server, Azure SQL Database y Azure SQL Data Warehouse.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: overview
author: markingmyname
ms.author: maghan
manager: craigg
ms.reviewer: alayu; sstein
ms.custom: seodec18, sqlfreshmay19
ms.date: 05/14/2019
ms.openlocfilehash: e93c417f286246f6db25d0463cec97eba8541c1c
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65993848"
---
# <a name="what-is-azure-data-studio"></a>¿Qué es Azure Data Studio?

Azure Data Studio es una multiplataforma herramienta de la base de datos para profesionales de datos con la familia de Microsoft de un entorno local y en la nube de plataformas de datos en Windows, MacOS y Linux.

Anteriormente se publicó en el nombre de vista previa de SQL Operations Studio, Azure Data Studio ofrece una experiencia de editor moderna con Intellisense, fragmentos de código, integración de control de código fuente y un terminal integrado. Se integra con el usuario de la plataforma de datos en mente, integrado en los gráficos de conjuntos de resultados de consulta y los paneles personalizables.

**[Descargue e instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)**


## <a name="sql-code-editor-with-intellisense"></a>Editor de código SQL con IntelliSense

[!INCLUDE[name-sos](../includes/name-sos-short.md)] ofrece una moderna, foco de teclado de SQL experiencia que facilita sus tareas diarias con características integradas, como ventanas de varias pestañas, un editor enriquecido de SQL, IntelliSense, finalización de la palabra clave, fragmentos de código, navegación de código y control de código fuente de codificación integración (Git). Ejecutar consultas SQL y a petición, ver y guardar los resultados como texto, JSON o Excel. Editar datos, organizar las conexiones de base de datos favoritas y examinar objetos de base de datos en un objeto familiar experiencia de exploración. Para obtener información sobre cómo usar el editor SQL, consulte [usar el editor SQL para crear objetos de base de datos](tutorial-sql-editor.md).

## <a name="smart-sql-code-snippets"></a>Fragmentos de código SQL inteligentes

Fragmentos de código SQL para generar la sintaxis SQL adecuada para crear bases de datos, tablas, vistas, procedimientos almacenados, los usuarios, inicios de sesión, roles, etc. y para actualizar los objetos de base de datos existente. Uso de fragmentos de código inteligentes para crear rápidamente copias de la base de datos para el desarrollo o con fines de prueba y para generar y ejecutar creación e INSERCIÓN secuencias de comandos.

[!INCLUDE[name-sos](../includes/name-sos-short.md)] También proporciona funcionalidad para crear fragmentos de código SQL personalizados. Para obtener más información, consulte [creación y uso de fragmentos de código](code-snippets.md).


## <a name="customizable-server-and-database-dashboards"></a>Servidor personalizable y los paneles de la base de datos

Cree paneles personalizables para supervisar y solucionar rápidamente los cuellos de botella de rendimiento en las bases de datos. Para obtener información acerca de los widgets de datos y paneles de la base de datos (y servidor), consulte [administrar servidores y bases de datos con los widgets de datos](insight-widgets.md).

## <a name="connection-management-server-groups"></a>Administración de conexiones (grupos de servidores)

Grupos de servidores proporcionan una manera de organizar la información de conexión para los servidores y se trabaja con bases de datos. Para obtener más información, consulte [grupos de servidores](server-groups.md).

## <a name="integrated-terminal"></a>Terminal integrado

Use sus herramientas favoritas de línea de comandos (por ejemplo, Bash, PowerShell, sqlcmd y bcp y ssh) en la ventana del Terminal integrado dentro de la [!INCLUDE[name-sos](../includes/name-sos-short.md)] interfaz de usuario. Para obtener información sobre el terminal integrado, consulte [terminal integrado](integrated-terminal.md).

## <a name="extensibility-and-extension-authoring"></a>Creación de la extensión y extensibilidad

Mejorar la [!INCLUDE[name-sos](../includes/name-sos-short.md)] experimentar extendiendo la funcionalidad de la instalación básica. [!INCLUDE[name-sos](../includes/name-sos-short.md)] proporciona puntos de extensibilidad para las actividades de administración de datos, así como soporte para la creación de la extensión.

Para obtener información acerca de la extensibilidad en [!INCLUDE[name-sos](../includes/name-sos-short.md)], consulte [extensibilidad](extensibility.md).
Para obtener información sobre la creación de extensiones, consulte [Extension authoring](extension-authoring.md).

## <a name="feature-comparison-with-sql-server-management-studio-ssms"></a>Comparación de características con SQL Server Management Studio (SSMS)

**Utilice Azure Data Studio si es:**
- Debe ejecutar en macOS o Linux
- Se conecta a un clúster de macrodatos de SQL Server 2019
- La mayor parte del tiempo de edición o la ejecución de consultas
- Necesita la capacidad de gráfico rápidamente y visualizar conjuntos de resultados
- Puede ejecutar la mayoría de las tareas administrativa a través del terminal integrado con sqlcmd o con Powershell
- Tiene una necesidad mínima para experiencias de Asistente
- No es necesario realizar configuración administrativa profunda

**Use SQL Server Management Studio si es:**
- Dedica la mayor parte de su tiempo en tareas de administración de bases de datos
- Está realizando la configuración administrativa profunda
- Está realizando la administración de seguridad, como la configuración de características de seguridad, evaluación de vulnerabilidades y administración de usuarios
- Utilizar los informes para SQL Server Query Store
- Tiene que usar de asesores de optimización de rendimiento y paneles
- Está realizando la importación y exportación de archivos dacpac
- Necesita acceso a servidores registrados y desea controlar SQL Server de servicios en Windows

### <a name="shell"></a>Shell

|Característica|Azure Data Studio |SSMS|
|:---|:---|:---|
|El inicio de sesión Azure|Sí|Sí|
|Panel|Sí||
|Extensiones|Sí||
|Terminal integrado|Sí||
|Explorador de objetos|Sí|Sí|
|Scripting de objetos|Sí|Sí|
|Sistema de proyectos|Sí||
|Seleccione en la tabla|Sí|Sí|
|Control de código fuente|Sí||
|Panel de tareas|Sí||
|Creación de temas|Sí||
|Modo oscuro|Sí||
|Explorador de recursos de Azure|Vista previa||
|Asistente para generar scripts||Sí|
|Importar y exportar DACPAC||Sí|
|Propiedades de objeto||Sí|
|Diseñador de tablas||Sí|


### <a name="query-editor"></a>Editor de consultas

|Característica|Azure Data Studio |SSMS|
|:---|:---|:---|
|Visor de gráficos|Sí||
|Resultados de la exportación a CSV, JSON, XLSX|Sí||
|IntelliSense|Sí|Sí|
|Fragmentos de código|Sí|Sí|
|Mostrar Plan|Vista previa|Sí|
|Estadísticas de clientes||Sí|
|Estadísticas de consultas activas||Sí|
|Opciones de consulta||Sí|
|Resultados a archivo||Sí|
|Resultados a texto||Sí|
|Visor espacial||Sí|
|SQLCMD||Sí|

### <a name="operating-system-support"></a>Sistemas operativos admitidos

|Característica|Azure Data Studio |SSMS|
|:---|:---|:---|
|Linux|Sí||
|macOS|Sí||
|Windows|Sí|Sí|

### <a name="data-engineering"></a>Ingeniería de datos

|Característica|Azure Data Studio |SSMS|
|:---|:---|:---|
|Crear a Asistente para la tabla externa|Vista previa||
|Integración de HDFS|Vista previa||
|PC de bolsillo|Vista previa||

### <a name="database-administration"></a>Administración de bases de datos

|Característica|Azure Data Studio |SSMS|
|:---|:---|:---|
|Copia de seguridad y restauración|Sí|Sí|
|Importación de archivos planos|Vista previa|Sí|
|Agente SQL|Vista previa|Sí|
|SQL Profiler|Vista previa|Sí|
|AlwaysOn||Sí|
|Always Encrypted||Sí|
|Asistente para copiar datos||Sí|
|Asesor de optimización de datos||Sí|
|Visor de registros de error||Sí|
|Planes de mantenimiento||Sí|
|Consulta de varios servidor||Sí|
|Administración basada en directivas||Sí|
|PolyBase||Sí|
|Almacén de consultas||Sí|
|Servidores registrados||Sí|
|REPLICATION||Sí|
|Administración de seguridad||Sí|
|Service Broker||Sí|
|SQL Mail||Sí|
|Template Explorer||Sí|
|Evaluación de vulnerabilidad||Sí|
|Administración de XEvent||Sí|

## <a name="next-steps"></a>Pasos siguientes

- [Descargue e instale [!INCLUDE[name-sos](../includes/name-sos-short.md)]](download.md)
- [Conectarse y consultar SQL Server](quickstart-sql-server.md)
- [Conectarse y consultar Azure SQL Database](quickstart-sql-database.md)

[!INCLUDE[get-help-sql-tools](../includes/paragraph-content/get-help-sql-tools.md)]

[!INCLUDE[contribute-to-content](../includes/paragraph-content/contribute-to-content.md)]