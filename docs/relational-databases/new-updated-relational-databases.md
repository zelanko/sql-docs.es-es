---
title: 'Actualizados: documentos de bases de datos relacionales | Microsoft Docs'
description: "Muestra fragmentos del contenido actualizado en la documentación de bases de datos relacionales que ha cambiado recientemente."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: 
ms.component: relational-databases-misc
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: 
ms.workload: relational-databases
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.author: genemi
ms.translationtype: HT
ms.sourcegitcommit: 834bba08c90262fd72881ab2890abaaf7b8f7678
ms.openlocfilehash: 70cb071dc7b6f4ff15c5c7dee3f24bb352d6eb61
ms.contentlocale: es-es
ms.lasthandoff: 10/02/2017

---
# <a name="new-and-recently-updated-relational-databases-docs"></a>Nuevos y actualizados recientemente: documentos de bases de datos relacionales
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]


Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **11-09-2017** &nbsp; a &nbsp; **27-09-2017**
- *Área temática:* &nbsp; **Bases de datos relacionales**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Importación y exportación de datos de SQL Server y de Azure SQL Database](import-export/overview-import-export.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Información general de los tipos de datos espaciales](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-spatial-data-types-overviewspatialspatial-data-types-overviewmd"></a>1. &nbsp; [Información general de los tipos de datos espaciales](spatial/spatial-data-types-overview.md)

*Actualizado: 26-09-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 27.  ms.author= "rickbyh".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 96dd44cf49e96d1d543a629d49de297dba9c1753 2e9629f852ea42a213c7c24831bcfa53e40358f2  (PR=0  ,  Filename=spatial-data-types-overview.md  ,  Dirpath=docs\relational-databases\spatial\  ,  MergeCommitSha40=b33976cf92f23fbb13cee0c353fd40608d002d94) -->



 -  Hay dos tipos de datos espaciales. El tipo de datos **geometry** admite datos planares o euclidianos (planisferio). El tipo de datos **geometry** se ajusta tanto a las características simples de Open Geospatial Consortium (OGC) para la especificación SQL versión 1.1.0 como a SQL MM (estándar ISO).
 -
 - Además, ..!NCLUDE-NotShown--ssNoVersion--../../includes/ssnoversion-md.md)] admite el tipo de datos **geography**, que almacena datos elipsoidales (tierra redonda), como coordenadas de latitud y longitud GPS.
 -
 -> [!IMPORTANT]
 ->  Para obtener una descripción detallada y ejemplos de las características espaciales introducidas en ..!NCLUDE-NotShown--ssSQL11--../../includes/sssql11-md.md)], incluidas las mejoras en los tipos de datos espaciales, descargue las notas del producto [New Spatial Features in SQL Server Code-Named "Denali"](http://go.microsoft.com/fwlink/?LinkId=226407) (Nuevas características espaciales en el código con el nombre "Denali" de SQL Server).
 -
 -##  <a name="objects"></a> Objetos de datos espaciales
 - Los tipos de datos **geometry** y **geography** admiten dieciséis objetos de datos espaciales o tipos de instancia. Pero solo se pueden *crear instancias*de once de estos tipos de instancia; puede crear y trabajar con estas instancias (o crear instancias de ellas) en una base de datos. Estas instancias obtienen determinadas propiedades de sus tipos de datos primarios que los distinguen como **Points**, **LineStrings, CircularStrings**, **CompoundCurves**, **Polygons**, **CurvePolygons** o como varias instancias de **geometry** o **geography** en una **GeometryCollection**. El tipo**Geography** tiene un tipo de instancia adicional, **FullGlobe**.
 -
 - La figura siguiente describe la jerarquía de **geometry** en la que se basan los tipos de datos **geometry** y **geography** . Los tipos a partir de los que pueden crearse instancias de **geometry** y **geography** se indican en azul.
 -
 - ![geom_hierarchy--../../relational-databases/spatial/media/geom-hierarchy.gif)
 -
 - Como la figura indica, los diez tipos a partir de los que pueden crearse instancias de los tipos de datos **geometry** y **geography** son **Point**, **MultiPoint**, **LineString**, **CircularString**, **MultiLineString**, **CompoundCurve**, **Polygon**, **CurvePolygon**, **MultiPolygon**y **GeometryCollection**. Existe un tipo adicional a partir del que pueden crearse instancias para el tipo de datos Geography: **FullGlobe**. Los tipos **geometry** y **geography** pueden reconocer una instancia concreta siempre y cuando se trate de una instancia bien formada, aunque no se haya definido explícitamente. Por ejemplo, si define una instancia **Point** usando explícitamente el método STPointFromText(), **geometry** y **geography** reconocen la instancia como **Point**, con tal de que la entrada de método esté bien formada. Si define la misma instancia mediante el método `STGeomFromText()` , los tipos de datos **geometry** y **geography** reconocen la instancia como **Point**.







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



