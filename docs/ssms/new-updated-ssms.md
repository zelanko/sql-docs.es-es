---
title: 'Actualizados: documentos de SSMS para SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Management Studio (SSMS) para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.author: genemi
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 15d706d713a813af8831c191aca85781a9c98472
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Nuevos y actualizados recientemente: SQL Server Management Studio (SSMS) para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **11-09-2017** &nbsp; a &nbsp; **27-09-2017**
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

1. [Descargar el módulo de PowerShell de SQL Server](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-powershell-moduledownload-sql-server-ps-modulemd"></a>1. &nbsp; [Descargar el módulo de SQL Server PowerShell](download-sql-server-ps-module.md)

*Actualizado: 26-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 37.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 3953870af5dca04eb3753e88a34fae69d365d6eb 10085b77284e957e34e5302975e5bc9cfd23fd0c  (PR=105  ,  Filename=download-sql-server-ps-module.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ed34b77d3f23e46c7736ef96c775990261290870) -->



Si la ejecución se realiza como administrador y el módulo se instala para todos los usuarios del equipo:

> Install-Module -Name SqlServer -AllowClobber

Si la ejecución no se puede realizar como administrador o la instalación se realiza solo para el usuario actual:

> Install-Module -Name SqlServer -Scope CurrentUser -AllowClobber

Si hay versiones actualizadas disponibles del módulo SqlServer, puede actualizar la versión con el comando Update-Module:

> Update-Module -Name SqlServer

Para ver las versiones del módulo instalado en el equipo, puede usar:

> Get-Module SqlServer -ListAvailable

Para usar una versión específica del módulo en los scripts, puede importarla con:

> Import-Module SqlServer -Version 21.0.17178








## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (0+1): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (0+1): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + actualizados (4+1): documentos de **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (17+0): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (3+0): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (1+1): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (2+0): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+1): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + actualizados (0+0): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



