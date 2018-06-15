---
title: 'Actualizados: documentos de SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: sql-server
ms.date: 04/28/2018
ms.openlocfilehash: 9ccf32a232b501bb3184786af0c48dc7214b1936
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32686655"
---
# <a name="new-and-recently-updated-sql-server-docs"></a>Nuevos y actualizados recientemente: documentos de SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área temática:* &nbsp; **SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Cómo colaborar en la documentación de SQL Server](sql-server-docs-contribute.md)
2. [Complemento de privacidad de SQL Server](sql-server-privacy.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Notas de la versión de SQL Server 2012 Service Pack](#TitleNum_1)
2. [Notas de la versión de SQL Server 2016](#TitleNum_2)
3. [Documentación de SQL Server](#TitleNum_3)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2012-service-pack-release-notessql-server-2012-sp4-release-notesmd"></a>1. &nbsp; [Notas de la versión de SQL Server 2012 Service Pack](sql-server-2012-sp4-release-notes.md)

*Actualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 57.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 ce108992ea942b4a11f30d67a1a52d7f26868caa a6269ba2cb2d3b3b54aebf5087dc4d513e476a96  (PR=5676  ,  Filename=sql-server-2012-sp4-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- **Creación de particiones de soft-NUMA automática**: con SQL 2014 SP2, se presenta la creación de particiones de [soft-NUMA](https://msdn.microsoft.com/library/ms345357(SQL.120).aspx) automática cuando la marca de seguimiento 8079 está habilitada en el nivel de servidor. Cuando la marca de seguimiento 8079 está habilitada durante el inicio, SQL Server 2014 SP2 interroga al diseño de hardware y configura automáticamente soft-NUMA en los sistemas que notifican ocho o más CPU por nodo NUMA. El comportamiento de soft-NUMA automática reconoce el hiperproceso (procesador HT/lógico). La creación de particiones y la creación de nodos adicionales escala el procesamiento en segundo plano al aumentar el número de agentes de escucha, escalado y capacidades de red y cifrado. Se recomienda probar primero el rendimiento de la carga de trabajo con soft-NUMA automática antes de activarla en producción.

**Notas de la versión del Service Pack 3**


**Páginas de descarga**

- [SQL Server 2012 SP3 Feature Pack](http://go.microsoft.com/fwlink/?linkid=615935)
- [SQL Server 2012 SP3 Express](http://go.microsoft.com/fwlink/?linkid=692144)

Para obtener más información para identificar la ubicación y el nombre del archivo que quiere descargar en función de la versión instalada actualmente, vea la sección "Seleccione el archivo correcto para descargar e instalar" en [Información de la versión de SQL Server 2012 Service Pack 3](https://support.microsoft.com/help/3072779/sql-server-2012-service-pack-3-release-information).

**Notas de la versión del Service Pack 2**


**Páginas de descarga**

- [SQL Server 2012 SP2 Feature Pack](http://go.microsoft.com/fwlink/?LinkID=401008)
- [SQL Server 2012 SP2 Express](http://go.microsoft.com/fwlink/?LinkID=401007)

Use la tabla siguiente para determinar la ubicación y el nombre del archivo que debe descargar en función de la versión que tenga instalada actualmente. Las páginas de descarga contienen los requisitos del sistema e instrucciones básicas para la instalación.

|Si la versión instalada actualmente es...|Y desea...|Descargue e instale...|



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-2016-release-notessql-server-2016-release-notesmd"></a>2. &nbsp; [Notas de la versión de SQL Server 2016](sql-server-2016-release-notes.md)

*Actualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Siguiente](#TitleNum_3))

<!-- Source markdown line 25.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 a15210866acf524dae49f3a7fd7957c9ffa6a78a 7257cb2017779242cbb8fa2b562f4b102502e942  (PR=5695  ,  Filename=sql-server-2016-release-notes.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->



  En este artículo se describen las limitaciones y los problemas de las versiones de SQL Server 2016, incluidos los Service Packs. Para obtener más información sobre las novedades, vea el artículo de [novedades de SQL Server 2016](https://docs.microsoft.com/sql/sql-server/what-s-new-in-sql-server-2016).

- Descargar SQL Server 2016 desde el **[Centro de evaluación](https://www.microsoft.com/evalcenter/evaluate-sql-server-2016)**
- Azure Virtual Machine pequeña ¿Tiene una cuenta de Azure?  Si es así, vaya **[aquí](https://azure.microsoft.com/marketplace/partners/microsoft/sqlserver2016sp1standardwindowsserver2016/)** para poner en marcha una máquina virtual con SQL Server 2016 SP1 ya instalado.
- Descargar SSMS Para obtener la versión más reciente de SQL Server Management Studio, consulte **[Descarga de SQL Server Management Studio (SSMS)]**.

**<a name="bkmk_2016sp2"></a>SQL Server 2016 Service Pack 2 (SP2)**


SQL Server 2016 SP2 incluye todas las actualizaciones acumulativas publicadas después de 2016 SP1, hasta e incluyendo CU8.

- [Microsoft Download SQL Server 2016 Service Pack 2 (SP2)](https://go.microsoft.com/fwlink/?linkid=869608)
- Para obtener una lista completa de las actualizaciones, vea [Información de versión de Service Pack 2 de SQL Server de 2016](https://support.microsoft.com/help/4052908/sql-server-2016-service-pack-2-release-information).



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-documentationsql-server-technical-documentationmd"></a>3. &nbsp; [Documentación de SQL Server](sql-server-technical-documentation.md)

*Actualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2))

<!-- Source markdown line 77.  ms.author= craigg.  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0262010ba39785a6d46b42f8469fb17701f13008 c69a83236391d039381a93c65ebbb2efa53e11b8  (PR=5695  ,  Filename=sql-server-technical-documentation.md  ,  Dirpath=docs\sql-server\  ,  MergeCommitSha40=d1c114b98fea55d2d4829dffdb25daf1b3f73dc2) -->




<!-- : : : m-r -->
**Probar SQL Server**
- Descargar desde el Centro de evaluación: [Descargar SQL Server para Windows](http://go.microsoft.com/fwlink/?LinkID=829477)
- Descargar desde el Centro de evaluación: Descargar SQL Server Management Studio (SSMS)
- Descargar desde el Centro de evaluación: Descargar SQL Server Data Tools (SSDT)
- Creación de una máquina virtual: [Obtener una máquina virtual con SQL Server](https://azure.microsoft.com/services/virtual-machines/sql-server/?wt.mc_id=sqL16_vm)





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

