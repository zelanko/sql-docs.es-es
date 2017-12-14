---
title: 'Actualizados: documentos de SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: sql-non-specified
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.author: genemi
ms.openlocfilehash: 77a97d94d005b43bf4c1a313a15a501cbe74a216
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sql-server-docs"></a>Nuevos y actualizados recientemente: documentos de SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área temática:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Asociados de desarrollo de SQL Server](partner-dev-sql-server.md)
2. [Asociados de alta disponibilidad y recuperación ante desastres de SQL Server](partner-hadr-sql-server.md)
3. [Asociados de administración de SQL Server](partner-management-sql-server.md)
4. [Asociados de supervisión de SQL Server](partner-monitor-sql-server.md)
5. [Notas de la versión de SQL Server 2012 SP4](sql-server-2012-sp4-release-notes.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Notas de la versión de SQL Server 2017](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp; [Notas de la versión de SQL Server 2017](sql-server-2017-release-notes.md)

*Actualizado: 20-11-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 37.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c9ac7e027e32b17bb9b54a4a878f70a70404f1cb 5b1aa8dc715fbb08d82b241f1e47f6e443b3e2fc  (PR=4032  ,  Filename=sql-server-2017-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



- **Solución alternativa:** en primer lugar, reinicie el equipo y compruebe si el recurso compartido de red FILESTREAM está disponible. Si el recurso compartido aún no está disponible, realice los siguientes pasos:

    1. En el Administrador de configuración de SQL Server, haga clic con el botón derecho en la instancia de SQL Server y haga clic en **Propiedades**.
    2. En la pestaña **FILESTREAM**, dedsactive **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos** y después haga clic en **Aplicar**.
    3. Seleccione **Habilitar FILESTREAM para el acceso de transmisión por secuencias de E/S de archivos** de nuevo con el nombre del recurso compartido original y haga clic en **Aplicar**.

**Master Data Services (MDS)**

- **Problema e impacto en el cliente:** en la página de permisos de usuario, al conceder permisos al nivel de raíz en la vista de árbol de entidades, verá el siguiente error: `"The model permission cannot be saved. The object guid is not valid"`.

- **Soluciones alternativas:**
  - Conceda permisos a los subnodos en la vista de árbol en lugar de a nivel de raíz.
  - o bien
  - Ejecute el script descrito en el blog del equipo de MDS sobre el [error al aplicar los permisos en el nivel de entidad](http://sqlblog.com/blogs/mds_team/archive/2017/09/05/sql-server-2016-sp1-cu4-regression-error-while-applying-permission-on-entity-level-quick-workaround.aspx).

**Analysis Services**

- **Problema e impacto sobre el cliente:** los conectores de datos de los siguientes orígenes aún no están disponibles para los modelos tabulares en el nivel de compatibilidad 1400.
  - Amazon Redshift
  - IBM Netezza
  - Impala
- **Solución alternativa** : ninguna.

- **Problema e impacto en el cliente:** los modelos de DirectQuery con el nivel de compatibilidad 1400 con perspectivas pueden generar errores al consultar o detectar metadatos.
- **Solución alternativa:** elimine las perspectivas y vuelva a implementar.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (3+14): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (87+0): documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + Actualizados (5+4): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (0+1): documentos de **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + Actualizados (2+2): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + Actualizados (10+9): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + Actualizados (2+4): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + Actualizados (4+2): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + Actualizados (0+1): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (21+0): documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + Actualizados (5+1): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (1+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + Actualizados (0+2): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


