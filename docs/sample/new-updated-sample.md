---
title: "Actualizado: ejemplo de documentación de SQL Server | Documentos de Microsoft"
description: "Mostrar fragmentos de contenido actualizado para obtener documentación modificado recientemente en, de ejemplo para Microsoft SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.service: 
ms.component: samples
ms.suite: sql
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 09/27/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.author: genemi
ms.workload: sample
ms.openlocfilehash: 363cb5dde93c628317a977082fe8697af890d51c
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="new-and-recently-updated-sample-for-sql-server"></a>Nuevos y actualizados recientemente: ejemplo de SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-09-28** &nbsp; - a - &nbsp; **2017-12-02**
- *Área de asunto:* &nbsp; **ejemplo para SQL Server**.




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

1. [Catálogo de base de datos WideWorldImporters](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-wideworldimporters-database-catalogworld-wide-importersdatabase-catalog-oltpmd"></a>1. &nbsp;[WideWorldImporters catálogo de base de datos](world-wide-importers/database-catalog-oltp.md)

*Actualizado: 2017-11-20* &nbsp; &nbsp; &nbsp; &nbsp;&nbsp; 

<!-- Source markdown line 136.  ms.author= "barbkess".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c055d0483699f06b8766ac2c999101934c14c55c 6975d5a3d1ade7b0ce34bd165bc0e9ef49299ba2  (PR=4032  ,  Filename=database-catalog-oltp.md  ,  Dirpath=docs\sample\world-wide-importers\  ,  MergeCommitSha40=7f8aebc72e7d0c8cff3990865c9f1316996a67d5) -->



Siempre que sea posible, la base de datos coloca las tablas que habitualmente se consultan juntos en el mismo esquema para minimizar la complejidad de la combinación.

El esquema de base de datos ha sido generado por el código en función de una serie de tablas de metadatos en otra base de datos WWI_Preparation. Esto proporciona WideWorldImporters un elevado grado de coherencia de diseño, nomenclatura coherencia e integridad. Para obtener más información sobre cómo se ha generado el esquema, vea el código fuente: [todo el mundo-importadores/wwi-base de datos-secuencias de comandos](https://github.com/Microsoft/sql-server-samples/tree/master/samples/databases/wide-world-importers/sample-scripts)

**Diseño de tabla**


- Todas las tablas con claves principales de columna única por motivos de simplicidad de combinación.
- Todos los esquemas, tablas, columnas, índices y restricciones check tienen una descripción de la propiedad que puede usarse para identificar el propósito del objeto o columna extendida. Tablas optimizadas en memoria son una excepción a esto ya que no admitan actualmente las propiedades extendidas.
- Todas las claves externas se indizan automáticamente a menos que haya otro índice no clúster que tenga el mismo componente izquierdo.
- Numeración automática en las tablas se basa en secuencias. Estas secuencias son más fáciles de trabajar con entre los servidores vinculados y entornos similares a las columnas de identidad. Tablas optimizadas en memoria utilizan las columnas de identidad ya que no admiten en SQL Server 2016.
- Una única secuencia (TransactionID) se usa para estas tablas: CustomerTransactions, SupplierTransactions y StockItemTransactions. Esto demuestra cómo un conjunto de tablas puede tener una única secuencia.
- Algunas columnas tienen valores predeterminados adecuados.

**Esquemas de seguridad**


Para la seguridad, WideWorldImporters no permite acceso directo a los esquemas de los datos de las aplicaciones externas. Para aislar el acceso, WideWorldImporters utiliza los esquemas de acceso de seguridad que no contienen datos, pero contienen vistas y procedimientos almacenados. Las aplicaciones externas utilizan los esquemas de seguridad para recuperar los datos que se pueden ver.  De esta manera, los usuarios solo pueden ejecutar las vistas y procedimientos almacenados en los esquemas de acceso seguro







## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
    2017-12-02  23:00pm
-->

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 14): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (87 + 0): **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (4 de 5 +): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (0 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (2 + 2): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (10 + 9): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (2 + 4): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (4 + 2): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (0 + 1): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (21 + 0): **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (5 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (1 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos y actualizados (0 + 0): **datos migración Ayudante (DMA) para SQL** documentos](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


