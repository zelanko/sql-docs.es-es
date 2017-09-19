---
title: 'Actualizados: documentos de SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/11/2017
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: bd22355518bde09b5af006062b2ec03cf11a7597
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>Nuevos y actualizados recientemente: documentos de SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **18-07-2017** &nbsp; a &nbsp; **11-09-2017**
- *Área temática:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [SQL Server 2008 R2 SP2 Release Notes](sql-server-2008-r2-sp2-release-notes.md)
2. [Notas de la versión de SQL Server 2012](sql-server-2012-release-notes.md)
3. [SQL Server 2012 SP1 Release Notes](sql-server-2012-sp1-release-notes.md)
4. [SQL Server 2012 SP2 Release Notes](sql-server-2012-sp2-release-notes.md)
5. [Notas de la versión de SQL Server 2012 SP3](sql-server-2012-sp3-release-notes.md)
6. [SQL Server 2014 Release Notes](sql-server-2014-release-notes.md)
7. [Visor de Ayuda y contenido sin conexión para SQL Server](sql-server-help-installation.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compacta proporciona vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Novedades de SQL Server 2016](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-whats-new-in-sql-server-2016what-s-new-in-sql-server-2016md"></a>1. &nbsp;[Novedades de SQL Server 2016](what-s-new-in-sql-server-2016.md)

*Actualizado: 08-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 34.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 e5bc0c05f120289f09a535400a4d521e4113ae55 0607d0a9af1c9a8dd9d3d7b0606895ff23bbffdc  (PR=0  ,  Filename=what-s-new-in-sql-server-2016.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=b97cc9723d563b19c85661f5ad7049a96fc904ff) -->



- Descargue la edición **gratuita** [**SQL Server 2016 Developer**](https://www.microsoft.com/en-us/cloud-platform/sql-server-editions-developers).
- Descargue la última versión de [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx).
- ¿Tiene una cuenta de Azure? Ponga en marcha una [máquina virtual con SQL Server 2016 ya instalado](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/).

**Motor de base de datos de SQL Server 2016**

- Ya puede configurar **varios archivos de base de datos tempDB** durante la instalación y configuración de SQL Server.
- El nuevo **Almacén de consultas** almacena los textos de las consultas, los planes de ejecución y las métricas de rendimiento dentro de la base de datos, lo que permite supervisar y solucionar los problemas de rendimiento con facilidad. Las consultas que consumen más tiempo, memoria o recursos de CPU se muestran en un panel.
- Las **tablas temporales** son tablas de historial en las que se registran todos los cambios de datos, junto con la fecha y hora en que se produjeron.
- La nueva **compatibilidad de JSON** integrada en SQL Server admite importaciones, exportaciones, análisis y almacenamiento de JSON.
- El nuevo motor de consultas de **PolyBase** integra SQL Server con datos externos en Hadoop o Azure Blob Storage. Puede importar y exportar datos, así como ejecutar consultas.
- La nueva característica **Stretch Database** permite archivar datos de forma dinámica y segura desde una base de datos de SQL Server local a una instancia de Azure SQL Database en la nube. SQL Server consulta automáticamente los datos locales y remotos en las bases de datos vinculadas.
- **OLTP en memoria:**
    - Ahora admite las restricciones FOREIGN KEY, UNIQUE y CHECK, los procedimientos almacenados compilados nativos OR, NOT, SELECT DISTINCT y OUTER JOIN y también las subconsultas en SELECT.
    - Admite tablas de hasta 2 TB (a partir de 256 GB).
    - Presenta mejoras del índice de almacenamiento de columnas para fines de ordenación y compatibilidad para el grupo de disponibilidad AlwaysOn.
- Nuevas características de seguridad:
    - **Always Encrypted:** cuando se habilita, solo la aplicación que tiene la clave de cifrado puede acceder a la información confidencial cifrada en la base de datos de SQL Server 2016. La clave nunca se pasa a SQL Server.







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + actualizados (3+12): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (5+0): documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (5+1): documentos de **Motor de base de datos para SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (19+82): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (1+8): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (12+1): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (0+1): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (7+1) : documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (1+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (0+2): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (1+4): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (4+1): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Nuevos + actualizados (0+1): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



