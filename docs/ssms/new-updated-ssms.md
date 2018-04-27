---
title: 'Actualizados: documentos de SSMS para SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Management Studio (SSMS) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql
ms.component: ssms
ms.date: 02/03/2018
ms.openlocfilehash: 8f2ad52b9741a3220a8c5db0a60924a41cc62d27
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Nuevos y actualizados recientemente: SQL Server Management Studio (SSMS) para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-12-2017** &nbsp; al &nbsp; **03-02-2018**
- *Área temática:* &nbsp; **SQL Server Management Studio (SSMS)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Instalación de versiones de idioma de SQL Server Management Studio (SSMS) distintas del inglés](install-other-languages.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Descarga de SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [SQL Server Management Studio - Changelog (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [Descarga de SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Actualizado: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 83.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 0e123e7bdf04f02fcd26ac31fa30ed5f31b19c7d 924246b55d3cad6a5d068da8a41f4be23dcfeb2b  (PR=4652  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



SSMS 17.4 es la versión más reciente de SQL Server Management Studio. La generación 17.x de SSMS proporciona compatibilidad con casi todas las áreas de características de SQL Server 2008 a SQL Server 2017. La versión 17.x también es compatible con PaaS de SQL Analysis Services.

La versión 17.4 incluye:

Evaluación de vulnerabilidad:
- Se ha incluido un nuevo servicio de evaluación de vulnerabilidades de SQL para analizar las bases de datos con objeto de encontrar posibles vulnerabilidades y desviaciones con respecto a los procedimientos recomendados, como errores de configuración, permisos excesivos y datos confidenciales sin protección.
- Los resultados de la evaluación incluyen pasos que requieren acción con los que se corrige cada problema y scripts de solución personalizados cuando proceda. El informe de evaluación se puede personalizar para ajustarse a cada entorno y adaptarse a los requisitos particulares. Obtenga más información en [Evaluación de vulnerabilidades de SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Se ha corregido un problema en el que *HasMemoryOptimizedObjects* iniciaba una excepción en Azure.
- Se ha agregado compatibilidad con la nueva característica CATALOG_COLLATION.

Panel AlwaysOn:
- Mejoras en el análisis de latencia de Grupos de disponibilidad.
- Se han agregado dos informes nuevos: *AlwaysOn\_Latency\_Primary* y *AlwaysOn\_Latency\_Secondary*.

Plan de presentación:
- Se han actualizado los vínculos para que apunten a la documentación correcta.
- Se permite el análisis de plan único directamente desde plan real generado.
- Nuevo conjunto de iconos.
- Se ha agregado compatibilidad para identificar "operadores lógicos de aplicación" como GbApply o InnerApply.

XE Profiler:
- Se ha cambiado el nombre a generador de perfiles XEvent.
- Ahora, los comandos de menú Iniciar y Detener inician o detienen la sesión de forma predeterminada.
- Se han habilitado métodos abreviados de teclado (como CTRL+F para realizar búsquedas).
- Se han agregado las acciones database\_name y client\_hostname a los eventos pertinentes en las sesiones del generador de perfiles XEvent. Para que el cambio surta efecto, puede que sea necesario eliminar las instancias de sesión QuickSessionStandard o QuickSessionTSQL existentes en los servidores (vea el [artículo 3142981 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3142981)).



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>2. &nbsp; [SQL Server Management Studio - Changelog (SSMS) (SQL Server Management Studio: registro de cambios (SSMS))](sql-server-management-studio-changelog-ssms.md)

*Actualizado: 29-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b5096fa8f1ae3f2e4bc040f43cb8810d96f2c69c eb641ac39386a26a76dc303f5bd55eb3f9f4c78d  (PR=0  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=ba4b1c2e5200f2f78786b710da18fd38fedde6c9) -->



**[SSMS 17.4](download-sql-server-management-studio-ssms.md)**

Disponible con carácter general | Número de compilación: 14.0.17213.0

**Novedades**


**SSMS general**

Evaluación de vulnerabilidad:
- Se ha incluido un nuevo servicio de evaluación de vulnerabilidades de SQL para analizar las bases de datos con objeto de encontrar posibles vulnerabilidades y desviaciones con respecto a los procedimientos recomendados, como errores de configuración, permisos excesivos y datos confidenciales sin protección.
- Los resultados de la evaluación incluyen pasos que requieren acción con los que se corrige cada problema y scripts de solución personalizados cuando proceda. El informe de evaluación se puede personalizar para ajustarse a cada entorno y adaptarse a los requisitos particulares. Obtenga más información en [Evaluación de vulnerabilidades de SQL](https://docs.microsoft.com/sql/relational-databases/security/sql-vulnerability-assessment).

SMO:
- Se ha corregido un problema en el que *HasMemoryOptimizedObjects* iniciaba una excepción en Azure.
- Se ha agregado compatibilidad con la nueva característica CATALOG_COLLATION.

Panel AlwaysOn:
- Mejoras en el análisis de latencia de Grupos de disponibilidad.
- Se han agregado dos informes nuevos: *AlwaysOn\_Latency\_Primary* y *AlwaysOn\_Latency\_Secondary*.

Plan de presentación:
- Se han actualizado los vínculos para que apunten a la documentación correcta.
- Se permite el análisis de plan único directamente desde plan real generado.
- Nuevo conjunto de iconos.
- Se ha agregado compatibilidad para identificar "operadores lógicos de aplicación" como GbApply o InnerApply.

XE Profiler:
- Se ha cambiado el nombre a generador de perfiles XEvent.
- Ahora, los comandos de menú Iniciar y Detener inician o detienen la sesión de forma predeterminada.
- Se han habilitado métodos abreviados de teclado (como CTRL+F para realizar búsquedas).
- Se han agregado las acciones database\_name y client\_hostname a los eventos pertinentes en las sesiones del generador de perfiles XEvent. Para que el cambio surta efecto, puede que sea necesario eliminar las instancias de sesión QuickSessionStandard o QuickSessionTSQL existentes en los servidores (vea el [artículo 3142981 de Connect](https://connect.microsoft.com/SQLServer/feedback/details/3142981)).

Línea de comandos:
- Se ha agregado una nueva opción de línea de comandos ("-G") que sirve para conectar SSMS automáticamente a un servidor o a una base de datos por medio de la autenticación de Active Directory ("Integrado" o "Contraseña"). Para más información, vea [Ssms (Utilidad)](ssms-utility.md).







## <a name="similar-articles-about-new-or-updated-articles"></a>Artículos similares sobre artículos nuevos o actualizados

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).


#### <a name="subject-areas-that-do-have-new-or-recently-updated-articles"></a>Áreas temáticas *con* artículos nuevos o actualizados recientemente


- [Nuevos + actualizados (1+3): &nbsp;documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Analytics Platform System para SQL**](../analytics-platform-system/new-updated-analytics-platform-system.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **Conexión a SQL**](../connect/new-updated-connect.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos del **Motor de base de datos de SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + actualizados (12+1): **documentos de** Integration Services para SQL](../integration-services/new-updated-integration-services.md)
- [Nuevos + actualizados (6+2): &nbsp;documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + actualizados (15+0): **documentos de** PowerShell para SQL](../powershell/new-updated-powershell.md)
- [Nuevos + actualizados (2+9): &nbsp;documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + actualizados (1+0): &nbsp;documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **SQL Operations Studio**](../sql-operations-studio/new-updated-sql-operations-studio.md)
- [Nuevos + actualizados (1+1): &nbsp;documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + actualizados (0+1): &nbsp;documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + actualizados (1+2): &nbsp;documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + actualizados (0+2): &nbsp;documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)



#### <a name="subject-areas-that-do-not-have-any-new-or-recently-updated-articles"></a>Áreas temáticas que *no* tienen artículos nuevos o actualizados recientemente


- [Nuevos + Actualizados (0+0): documentos de **Data Migration Assistant (DMA) para SQL**](../dma/new-updated-dma.md)
- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + actualizados (0+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + actualizados (0+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../samples/new-updated-samples.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


