---
title: 'Actualizado: los documentos de T-SQL | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, Transact-SQL."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: t-sql
ms.date: 02/03/2018
ms.openlocfilehash: c1f1ce751bd4bca781644e7e2f5282320c8c88a8
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-transact-sql-docs"></a>Las nuevas y recientemente actualizado: los documentos de Transact-SQL



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-12-03** &nbsp; - a - &nbsp; **2018-02-03**
- *Área de asunto:* &nbsp; **T-SQL**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


***En este momento no hay ningún artículo nuevo en la lista.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [CREAR estadísticas (Transact-SQL)](#TitleNum_1)
2. [Actualizar estadísticas (Transact-SQL)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-create-statistics-transact-sqlstatementscreate-statistics-transact-sqlmd"></a>1. &nbsp;[CREATE STATISTICS (Transact-SQL)](statements/create-statistics-transact-sql.md)

*Actualizado: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 200.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 384e68493597bcc36876a3c7bada2630106256e2 c22168ea59b6020e8ebe1ccac5fa6a6049e6db4d  (PR=4460  ,  Filename=create-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*
**se aplica a**: SQL Server (a partir de SQL Server de 2017 CU3).

 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de estadística. Para obtener más información, vea [Configure the max degree of parallelism Server Configuration Option](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.

 *max_degree_of_parallelism* puede ser:

 1 Suprime la generación de planes paralelos.

 \>1 limita el número máximo de procesadores utilizados en una operación estadística paralelo al número especificado o menos, según la carga de trabajo del sistema actual.

 0 (valor predeterminado) utiliza el número real de procesadores o menos, según la carga de trabajo del sistema actual.

 \<update_stats_stream_option > identifica únicamente con fines informativos. No compatible. La compatibilidad con versiones posteriores no está garantizada.




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-update-statistics-transact-sqlstatementsupdate-statistics-transact-sqlmd"></a>2. &nbsp;[UPDATE STATISTICS (Transact-SQL)](statements/update-statistics-transact-sql.md)

*Actualizado: 2018-01-04* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 167.  ms.author= "edmaca".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 5721e21a9f43fa784fe9357c47cb2a814385e63d 24ae47c553635f389a182e5e643bf9bd6bf59e78  (PR=4460  ,  Filename=update-statistics-transact-sql.md  ,  Dirpath=docs\t-sql\statements\  ,  MergeCommitSha40=4aeedbb88c60a4b035a49754eff48128714ad290) -->



MAXDOP = *max_degree_of_parallelism*

**Se aplica a**: (a partir de SQL Server de 2017 CU3) de SQL Server.

 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de estadística. Para obtener más información, vea [Configure the max degree of parallelism Server Configuration Option](statements/../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.

 *max_degree_of_parallelism* puede ser:

 1 Suprime la generación de planes paralelos.

 \>1 limita el número máximo de procesadores utilizados en una operación estadística paralelo al número especificado o menos, según la carga de trabajo del sistema actual.

 0 (valor predeterminado) utiliza el número real de procesadores o menos, según la carga de trabajo del sistema actual.








## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas de asunto que *hacer* se nuevas o recientemente actualizado artículos


- [Nuevos y actualizados (1 + 3):&nbsp; **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **Analytics Platform System para SQL** documentos](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (12 + 1): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (6 + 2):&nbsp; **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (15 + 0): **PowerShell para SQL** documentos](../powershell/new-updated-powershell.md)
- [Nuevos y actualizados (2 + 9):&nbsp; **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (1 + 0):&nbsp; **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (1 + 1):&nbsp; **Studio de operaciones SQL** documentos](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos y actualizados (1 + 1):&nbsp; **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (0 + 1):&nbsp; **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (1 + 2):&nbsp; **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (0 + 2):&nbsp; **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Asunto áreas que realizan *no* cualquier nuevo o recientemente actualizaron artículos


- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos y actualizados (0 + 0): **ActiveX Data Objects (ADO) para SQL** documentos](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos y actualizados (0 + 0): **Data Quality Services para SQL** documentos](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos y actualizados (0 + 0): **extensiones de minería de datos (DMX) para SQL** documentos](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos y actualizados (0 + 0): **expresiones multidimensionales (MDX) para SQL** documentos](../mdx/new-updated-mdx.md)
- [Nuevos y actualizados (0 + 0): **ODBC (conectividad abierta de base de datos) para SQL** documentos](../odbc/new-updated-odbc.md)
- [Nuevos y actualizados (0 + 0): **ejemplos para SQL** documentos](../sample/new-updated-sample.md)
- [Nuevos y actualizados (0 + 0): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos y actualizados (0 + 0): **XQuery para SQL** documentos](../xquery/new-updated-xquery.md)


