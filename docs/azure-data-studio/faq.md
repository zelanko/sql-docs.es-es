---
title: Preguntas más frecuentes
titleSuffix: Azure Data Studio
description: Preguntas más frecuentes (P+F) sobre Azure Data Studio.
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: markingmyname
ms.author: maghan
ms.reviewer: alayu; sstein
ms.custom: seodec18
ms.date: 09/24/2018
ms.openlocfilehash: 1916a10a468fdc44c021e410eb1521cb7c219d58
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67959547"
---
# <a name="includeazure-data-studioincludesname-sosmd-faq"></a>[!INCLUDE[Azure Data Studio](../includes/name-sos.md)] PREGUNTAS MÁS FRECUENTES

## <a name="what-is-azure-data-studio"></a>¿Qué es Azure Data Studio?

Azure Data Studio está abierto un nuevo origen, el entorno de escritorio multiplataforma para profesionales de datos con la familia de datos de Azure de un entorno local y plataformas de datos en Windows, MacOS y Linux en la nube. Anteriormente se publicó en el nombre de vista previa de SQL Operations Studio, ofertas de Azure Data Studio un editor moderno experiencia con rayo rápido IntelliSense, fragmentos de código, integración de control de código fuente y un terminal integrado. Se integra con el usuario de la plataforma de datos en mente, integrado en los gráficos de conjuntos de resultados de consulta y los paneles personalizables.

Investigación ha demostrado que los usuarios dedican un orden de magnitud más tiempo a trabajar en la edición de consultas que en cualquier otra tarea con SQL Server Management Studio. Por ese motivo, Azure Data Studio se ha diseñado para centrarse profundamente en la funcionalidad que se usa más, con experiencias adicionales disponibles como extensiones opcionales en el producto. Esto permite que todos los usuarios personalizar su entorno para los flujos de trabajo que se usan con más frecuencia.


## <a name="how-much-does-azure-data-studio-cost"></a>¿Cuánto cuesta Azure Data Studio?

Azure Data Studio es gratuita para uso privado o comercial.

## <a name="who-should-use-azure-data-studio"></a>¿Quién debe usar Azure Data Studio

Cualquier persona puede usar Azure Data Studio. Sin embargo, está diseñado para simplificar las tareas realizadas por los desarrolladores de base de datos, los administradores de base de datos, los administradores del sistema y fabricantes independientes de software.

## <a name="what-can-i-do-with-azure-data-studio"></a>¿Qué puedo hacer con Azure Data Studio?

Azure Data Studio se basa en el código de Visual Studio y ofrece una ligera, experiencia de flujo de trabajo de código moderno de foco de teclado cuando se trabaja con SQL Server, Azure SQL Database, Azure SQL Data Warehouse. Azure Data Studio hace que las experiencias de núcleo que dependen de cada día simple y fácil con características integradas como ventanas de varias pestañas, un editor enriquecido de SQL, IntelliSense, finalización de la palabra clave, fragmentos de código & navegación de código e integración de control de código fuente (Git y TFS). Puede ejecutar consultas y a petición, ver & Guardar resultados como texto, JSON o Excel, editar datos, organizar & Administrar las conexiones de base de datos favoritas y examinar objetos de base de datos en un objeto familiar experiencia de exploración.

Use sus herramientas favoritas de línea de comandos (por ejemplo, Bash, PowerShell, sqlcmd, bcp, psql y ssh) en la ventana del Terminal integrado directamente en la interfaz de usuario de Azure Data Studio. Generar y ejecutar CREATE fácilmente y secuencias de comandos de INSERCIÓN para los objetos de base de datos crear copias de la base de datos para el desarrollo o con fines de prueba. Aumente su productividad con código inteligentes enriquecidas y fragmentos de código gráficas experiencias que crean nuevas bases de datos y objetos de base de datos (como tablas, vistas, procedimientos almacenados, los usuarios, inicios de sesión, roles, etc.) o actualizar los objetos de base de datos existentes. Use paneles personalizables enriquecidos para supervisar y solucionar rápidamente los cuellos de botella de rendimiento en las bases de datos local, en Azure o en cualquier nube.

Azure Data Studio ofrece una experiencia coherente para realizar copias de seguridad y restaurar las bases de datos. Con compatibilidad con grupos de disponibilidad de SQL Server Always-On planeada, fácilmente puede configurar, supervisar y solucionar problemas de grupos de disponibilidad para sus bases de datos de SQL Server críticas y rápida conmutación por error a una base de datos secundaria durante un desastre. Azure Data Studio se ha diseñado para mejorar la productividad en el ciclo de vida de DevOps de las bases de datos de elección en los sistemas operativos de su elección. Como resultado, siempre tiene el control, y puede reducir los riesgos, resolver problemas con mayor rapidez y entregar continuamente valor que supera las expectativas del cliente.

## <a name="is-azure-data-studio-open-source"></a>¿Es código abierto de datos de Azure Studio?

El código fuente de Azure Data Studio y sus proveedores de datos está disponible en GitHub. El código fuente para el front-end Data Studio de Azure (que se basa en Visual Studio Code) está disponible en un código fuente de términos de licencia que proporciona derechos para modificar y utilizar el software, pero no para redistribuir el control u hospedarlo en un servicio en la nube. El código fuente para los proveedores de datos está disponible bajo la licencia MIT en [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-we-plan-to-open-source-ssms"></a>¿Tenemos previsto SSMS de código abierto?

No. Sin embargo, nueva generación herramientas CLI y la GUI de vives son de código abierto. Por ejemplo, la extensión mssql para VS Code, mssql-generador de scripts y msql CLI son todo código abierto en GitHub. El código fuente de Azure Data Studio está disponible en GitHub.  

## <a name="now-that-there-is-azure-data-studio-does-microsoft-plan-to-deprecate-ssms-and-ssdt"></a>¿Ahora que hay datos de Azure Studio, Microsoft va a dejar de usar SSMS y SSDT? 

No. Se seguirán las inversiones en herramientas de Windows de estrella (SSMS, SSDT, PowerShell) además de la próxima generación de herramientas CLI y la GUI de multi-DB y vives. El objetivo es ofrecer a los clientes la posibilidad de utilizar las herramientas que deseen en las plataformas de su elección para sus escenarios. Azure Data Studio más estrechamente se centra en las experiencias en torno a la edición de consultas y el desarrollo de datos, qué investigaciones han demostrado es la capacidad de usa más intensivo en SQL Server Management Studio en un orden de magnitud. También están disponibles como extensiones en Azure Data Studio adicionales características administrativas de gran valor, como la copia de seguridad, restauración, administración de trabajos de agente y servidor de generación de perfiles. Azure Data Studio también es multiplataforma, lo que permite a los usuarios trabajar en su plataforma de elección. Sin embargo, SQL Server Management Studio todavía ofrece la gama más amplia de las funciones administrativas y sigue siendo la herramienta estrella para tareas de administración de plataforma. 

## <a name="when-should-i-use-azure-data-studio-vs-sql-server-management-studio"></a>¿Cuando se debe usar Azure Data Studio frente a SQL Server Management Studio?

*Utilice Azure Data Studio si es:*

- Dedica la mayor parte de su tiempo, editar o ejecutar consultas.
- Necesita la capacidad de gráfico rápidamente y visualizar conjuntos de resultados.
- Puede ejecutar la mayoría de las tareas administrativa a través del terminal integrado mediante sqlcmd o Powershell.
- Tienen una necesidad mínima para experiencias de asistente.
- No es necesario hacer profundo administrativa o configuración relacionados de la plataforma.
- Debe ejecutar en macOS o Linux.

*Use SQL Server Management Studio si es:*

- Dedican la mayor parte de su tiempo en tareas de administración de bases de datos.
- Está realizando una configuración compleja administrativa o la plataforma.
- Está realizando la administración de seguridad, como la configuración de características de seguridad, evaluación de vulnerabilidades y administración de usuarios.
- Tiene que usar de asesores de optimización de rendimiento y paneles.
- Utilice diagramas de base de datos y los diseñadores de la tabla.
- Está realizando la importación y exportación de archivos dacpac.
- Necesita acceso a los servidores registrados.
- Asegúrese de usar el modo sqlcmd, live estadísticas de consulta o las estadísticas de cliente.

## <a name="feature-comparison"></a>Comparación de características

### <a name="shell-features"></a>Características de shell

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|El inicio de sesión Azure|Sí|Sí|
|panel|Sí| |
|Extensiones|Sí| |
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
|Asistente para generar scripts||Sí
|Importar y exportar DACPAC||Sí|
|Propiedades de objeto||Sí|
|Diseñador de tablas||Sí|

### <a name="query-editor"></a>Editor de consultas

|Característica|Azure Data Studio|SSMS|
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
|Depurador de T-SQL||Sí|

### <a name="operating-system-support"></a>Sistemas operativos admitidos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Windows|Sí|Sí|
|macOS|Sí||
|Linux|Sí||

### <a name="data-engineering"></a>Ingeniería de datos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Asistente para datos externos|Vista previa||
|Integración de HDFS|Vista previa||
|PC de bolsillo|Vista previa||

### <a name="database-administration"></a>Administración de bases de datos

|Característica|Azure Data Studio|SSMS|
|:---|:---|:---|
|Copia de seguridad y restauración|Sí|Sí|
|Importación de archivos planos|Vista previa|Sí|
|Agente SQL|Vista previa|Sí|
|SQL Profiler|Vista previa|Sí|
|AlwaysOn||Sí|
|Always Encrypted||Sí|
|Asistente para copiar datos||Sí|
|Asesor de optimización de datos||Sí|
|Diagramas de base de datos||Sí|
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


## <a name="azure-data-studio-is-missing-a-feature-that-is-in-ssmsssdt-will-you-add-it"></a>Azure Data Studio le falta una característica que se encuentra en SSMS o SSDT. ¿Se lo agregará?

Depende de la necesidad de escenario de & cliente o business. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="i-understand-azure-data-studio-and-the-mssql-extension-for-vs-code-are-powered-by-a-new-tools-service-that-uses-smo-apis-under-the-covers-is-smo-available-on-linux-and-macos"></a>Entiendo que Studio de datos de Azure y la extensión mssql para VS Code cuentan con un nuevo servicio de las herramientas que usa las API de SMO en segundo plano. ¿Está disponible en Linux y macOS SMO?

La API SMO aún no están disponibles en Linux o macOS en forma de consumir. Hemos trasladado sobre un subconjunto de las API de SMO para .NET Core que necesitábamos para Azure Data Studio y se planea expandir como parte del mapa de ruta. El servicio de las herramientas de SQL se encuentra en GitHub: [ https://github.com/Microsoft/sqltoolsservice ](https://github.com/Microsoft/sqltoolsservice).

## <a name="do-you-plan-to-port-the-dacfx-apis-andor-sqlpackageexe-andor-ssdt-to-linux-and-macos"></a>¿Tiene pensado trasladar la DACFx APIs o sqlpackage.exe y SSDT para Linux y macOS?

Está en el plan a largo plazo. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="will-sql-powershell-cmdlets-be-available-on-linux-and-macos"></a>¿Estará disponible en Linux y macOS cmdlets de PowerShell de SQL?

PowerShell de SQL está disponible actualmente en la Galería de PowerShell y puede usarla en Windows para trabajar con SQL Server en ejecución en cualquier lugar, incluido SQL en Linux. Oferta de SQL PowerShell cmdlets en Linux y macOS es en el mapa de ruta. Para ayudar a priorizar, una sugerencia de archivos en [GitHub](https://github.com/microsoft/azuredatastudio/issues).

## <a name="who-usually-uses-azure-data-studio"></a>¿Normalmente, quién usa Azure Data Studio?

Los programadores y DBA normalmente son los usuarios de Azure Data Studio.

## <a name="does-azure-data-studio-integrate-with-azure-sql-data-warehouse"></a>¿Azure Data Studio se integra con Azure SQL Data Warehouse?

Sí. Soporte técnico de Azure Data Studio para Azure SQL Data Warehouse está actualmente en versión preliminar, junto con la instancia administrada de Azure SQL Database y SQL Server 2019 Big Data.

## <a name="why-is-azure-data-studio-important-for-the-new-version-of-sql-server"></a>¿Por qué es importante para la nueva versión de SQL Server Data Studio de Azure?

A medida que SQL Server extiende sus funcionalidades en el espacio de datos de gran tamaño, necesita herramientas nuevas para admitirlos casos de uso. Por ese motivo, Azure Data Studio hoy en día se envía una nueva experiencia de vista previa de la compatibilidad con SQL Server Big Data, incluida la primera experiencia de cuaderno alguna vez en el conjunto de herramientas de SQL Server y un nuevo Asistente para crear tabla externa que hace que el acceso a los datos de SQL remoto Instancias de servidor y Oracle fáciles y rápidas.
