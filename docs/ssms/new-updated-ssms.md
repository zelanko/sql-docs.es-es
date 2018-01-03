---
title: 'Actualizados: documentos de SSMS para SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Management Studio (SSMS) para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: ssms
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 12/02/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.author: genemi
ms.workload: ssms-sql-server-management-studio
ms.openlocfilehash: a1a9156ef4bc2846f377f9c0695ec015d58606dd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Nuevos y actualizados recientemente: SQL Server Management Studio (SSMS) para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]


Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **28-09-2017** &nbsp; a &nbsp; **02-12-2017**
- *Área temática:* &nbsp; **SQL Server Management Studio (SSMS)**.




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

1. [SQL Server Management Studio - Changelog (SSMS)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1. &nbsp; [SQL Server Management Studio - Changelog (SSMS) (SQL Server Management Studio: registro de cambios (SSMS))](sql-server-management-studio-changelog-ssms.md)

*Actualizado: 09-10-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f483a7e0ba53cff80d3f2d33c9196906d27a7a61 c125f43f0a45e70ce180e62edecc68bdcffd5086  (PR=3441  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=29122bdf543e82c1f429cf401b5fe1d8383515fc) -->



**[SSMS 17.3--download-sql-server-management-studio-ssms.md)**

Disponible con carácter general | Número de compilación: 14.0.17199.0

**Mejoras**


- Se ha agregado el nuevo asistente "Importar archivo plano" para simplificar la experiencia de importación de archivos CSV con un marco de trabajo inteligente, que ahora no exige prácticamente intervención por parte del usuario ni poseer conocimientos especializados sobre dominios. Para obtener más información, vea [Importar archivos planos mediante el asistente de SQL--../relational-databases/import-export/import-flat-file-wizard.md).
- Se ha agregado el nodo "XEvent Profiler" al Explorador de objetos. Para obtener más información, vea [Usar el Generador de eventos XEvent de SSMS--../relational-databases/extended-events/use-the-ssms-xe-profiler.md).
- Se han actualizado el filtrado y la categorización de esperas en el informe histórico de esperas del panel de rendimiento.
- Se ha agregado la comprobación de sintaxis de la función "Predict".
- Se ha agregado la comprobación de sintaxis de las consultas de administración de biblioteca externa.
- Se ha agregado compatibilidad con SMO a la administración de biblioteca externa.
- Se ha agregado compatibilidad con "Iniciar PowerShell" a la ventana "Servidores registrados" (se requiere un nuevo módulo de SQL PowerShell).
- Always On: se ha agregado [compatibilidad con enrutamiento de solo lectura--../database-engine/availability-groups/windows/configure-read-only-routing-for-an-availability-group-sql-server.md) para grupos de disponibilidad.
- Se ha agregado una opción para enviar detalles de seguimiento a la ventana de salida de los inicios de sesión "Active Directory - Universal compatible con MFA" (desactivados de forma predeterminada; deben activarse en la configuración de usuario, en "Herramientas > Opciones > Servicios de Azure > Nube de Azure > Nivel de seguimiento de la ventana de salida de ADAL").
- Almacén de consultas:
  - La interfaz de usuario del almacén de consultas será accesible aunque QDS esté desactivado, siempre que haya registrado datos.
  - La interfaz de usuario del almacén de consultas ahora expone la categorización de esperas en todos los informes existentes. Esto permite que los clientes desbloqueen los escenarios de consultas que más esperan y muchos otros.
- Se ha convertido en opcional la inclusión de los encabezados de parámetros de scripting (desactivada de forma predeterminada; se puede habilitar en la configuración de usuario, en "Herramientas > Opciones > Explorador de objetos de SQL Server > Scripting > Incluir encabezado de parámetros de scripting"). [Artículo de Connect 3139199](https://connect.microsoft.com/SQLServer/feedback/details/3139199).







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


