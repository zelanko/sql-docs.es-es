---
title: 'Actualizados: documentos de T-SQL | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente de Transact-SQL.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 04/28/2018
ms.openlocfilehash: b1bc891bf7edc4cd82c38c8d647c279828190298
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32725627"
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Nuevos y actualizados recientemente: documentos de Transact-SQL



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Tema:* &nbsp; **T-SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


***En este momento no hay ningún artículo nuevo en la lista.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](#TitleNum_1)
2. [Instrucciones RESTORE (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-alter-database-scoped-configuration-transact-sqlstatementsalter-database-scoped-configuration-transact-sqlmd"></a>1. &nbsp; [ALTER DATABASE SCOPED CONFIGURATION (Transact-SQL)](statements/alter-database-scoped-configuration-transact-sql.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 150.  ms.author= "carlrab".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f6833910b664d0059a9073589807b195052325b3 bf969f123b22e6ebc650380a6905156f26ed6ca6  (PR=0  ,  Filename=alter-database-scoped-configuration-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



XTP_PROCEDURE_EXECUTION_STATISTICS **=** { ON | **OFF** }

**Se aplica a**: *{Included-Content-Goes-Here}*

Habilita o deshabilita la recopilación de estadísticas de ejecución a nivel de módulo para los módulos de T-SQL compilados de forma nativa en la base de datos actual. El valor predeterminado es OFF. Las estadísticas de ejecución se reflejan en [sys.dm_exec_procedure_stats].

Las estadísticas de ejecución a nivel de módulo de los módulos de T-SQL compilados de forma nativa se recopilan si esta opción está activada o si se habilita la recopilación de estadísticas mediante [sp_xtp_control_proc_exec_stats].

XTP_QUERY_EXECUTION_STATISTICS **=** { ON | **OFF** }

**Se aplica a**: *{Included-Content-Goes-Here}*

Habilita o deshabilita la recopilación de estadísticas de ejecución a nivel de instrucción para los módulos de T-SQL compilados de forma nativa en la base de datos actual. El valor predeterminado es OFF. Las estadísticas de ejecución se reflejan en [sys.dm_exec_query_stats] y en el [Almacén de consultas].

Las estadísticas de ejecución a nivel de instrucción de los módulos de T-SQL compilados de forma nativa se recopilan si esta opción está activada o si se habilita la recopilación de estadísticas mediante [sp_xtp_control_query_exec_stats].

Para obtener información más detallada sobre la supervisión del rendimiento de los módulos de T-SQL compilados de forma nativa, consulte [Supervisar el rendimiento de los procedimientos almacenados compilados de forma nativa].



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-restore-statements-transact-sqlstatementsrestore-statements-transact-sqlmd"></a>2. &nbsp; [Instrucciones RESTORE (Transact-SQL)](statements/restore-statements-transact-sql.md)

*Actualizado: 13-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 339.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 2902efb58bb964d3e9a0660956690d37f0397c00 36186a7cffd26ffa54a83e383ffd752dbc568a4d  (PR=0  ,  Filename=restore-statements-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=f70f24bff1677b33c661abd13726f491ce32b305) -->



**Notas generales: Instancia administrada de SQL Database**


En el caso de una restauración asincrónica, la restauración continúa incluso si se interrumpe la conexión del cliente. Si la conexión se interrumpe, puede comprobar la vista [sys.dm_operation_status] del estado de una operación de restauración (así como para las bases de datos CREATE y DROP).

Las siguientes opciones de base de datos se establecen/invalidan y no se pueden cambiar más adelante:

- NEW_BROKER (si el agente no está habilitado en el archivo .bak)
- ENABLE_BROKER (si el agente no está habilitado en el archivo .bak)
- AUTO_CLOSE=OFF (si una base de datos del archivo .bak tiene AUTO_CLOSE=ON)
- RECOVERY FULL (si una base de datos del archivo .bak tiene el modo de recuperación SIMPLE o BULK_LOGGED)
- Se agrega un grupo de archivos optimizado para memoria, al que se asigna el nombre XTP si no estaba en el archivo .bak de origen. Se cambia el nombre de todos los grupos de archivos optimizados para memoria existentes a XTP
- Las opciones SINGLE_USER y RESTRICTED_USER se convierten en MULTI_USER

**Limitaciones: Instancia administrada de SQL Database**

Se aplican las siguientes limitaciones:

- Los archivos .BAK que contienen varios conjuntos de copia de seguridad no se pueden restaurar.
- Los archivos .BAK que contienen varios archivos de registro no se pueden restaurar.
- Se producirá un error en la restauración si el archivo .bak contiene datos FILESTREAM.
- Las copias de seguridad que contienen bases de datos que tienen objetos en memoria activos no se pueden restaurar en estos momentos.
- Las copias de seguridad que contienen bases de datos en las que en algún momento ha habido objetos en memoria no se pueden restaurar en estos momentos.
- Las copias de seguridad que contienen bases de datos en modo de solo lectura no se pueden restaurar en estos momentos. Esta limitación se quitará próximamente.

Para más información, consulte [Instancia administrada].







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).



#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (11+6): documentos de &nbsp;&nbsp;**Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (18+0): documentos de &nbsp;&nbsp;**Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + actualizados (218+14): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (14+0): documentos del &nbsp;&nbsp;**Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (3+2): documentos de &nbsp;&nbsp;**Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (3+3): documentos de &nbsp;&nbsp;**Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (7+10): documentos de&nbsp;&nbsp;**Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (0+2): documentos de &nbsp;&nbsp;**Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (1+3): documentos de &nbsp;&nbsp;**SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + actualizados (2+3): documentos de &nbsp;&nbsp;**Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (1+1): documentos de &nbsp;&nbsp;**SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (5+2): documentos de &nbsp;&nbsp;**SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+2): documentos de &nbsp;&nbsp;**Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Nuevos + actualizados (1+1): documentos de &nbsp;&nbsp;**Herramientas para SQL**](../tools/new-updated-tools.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (0+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../samples/new-updated-samples.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)

