---
title: 'Actualizados: documentos de SSMS para SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Management Studio (SSMS) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssms
ms.date: 04/28/2018
ms.openlocfilehash: 1ce446219f71baca0f4cdedc835fca929b572a0f
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Nuevos y actualizados recientemente: SQL Server Management Studio (SSMS) para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área temática:* &nbsp; **SQL Server Management Studio (SSMS)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Tutorial: Conexión a una instancia de SQL Server y realización de consultas con SQL Server Management Studio](tutorials/connect-query-sql-server.md)
2. [Tutorial: Creación de scripts de objetos en SQL Server Management Studio](tutorials/scripting-ssms.md)
3. [Tutorial: Componentes y configuración de SQL Server Management Studio](tutorials/ssms-configuration.md)
4. [Tutorial: Otras recomendaciones y trucos al usar SSMS](tutorials/ssms-tricks.md)
5. [Tutorial: Uso de plantillas en SQL Server Management Studio](tutorials/templates-ssms.md)



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
2. [Tutoriales de SQL Server Management Studio (SSMS)](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>1. &nbsp; [SQL Server Management Studio - Changelog (SSMS) (SQL Server Management Studio: registro de cambios (SSMS))](sql-server-management-studio-changelog-ssms.md)

*Actualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 27.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 eb641ac39386a26a76dc303f5bd55eb3f9f4c78d f560f09b51ea30b255c10f7eb86857c3090881d9  (PR=5676  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**SSMS 17.6**


Número de versión: 17.6<br>
Número de compilación: 14.0.17230.0<br>
Fecha de lanzamiento: 20 de marzo de 2018

**Novedades**


**SSMS general**

Instancia administrada de SQL Database:

- Se ha agregado compatibilidad para [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance). Instancia administrada de Azure SQL Database (versión preliminar) es una nueva opción de Azure SQL Database, que proporciona una compatibilidad cercana al 100% con SQL Server local, una implementación nativa de [red virtual (VNet)](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview) que aborda cuestiones de seguridad comunes y un [modelo empresarial](https://azure.microsoft.com/pricing/details/sql-database/) favorable para los clientes de SQL Server local.
- Compatibilidad con escenarios de administración habituales como los siguientes:
   - Creación y modificación de bases de datos.
   - Copias de seguridad y restauración de bases de datos.
   - Importación, exportación, extracción y publicación de aplicaciones de capa de datos.
   - Consulta y modificación de propiedades del servidor.
   - Compatibilidad total con el Explorador de objetos.
   - Creación de scripts de objetos de base de datos.
   - Compatibilidad con Trabajos del Agente SQL.
   - Compatibilidad con los servidores vinculados.
- Obtenga más información sobre Instancias administradas [aquí](https://azure.microsoft.com/blog/migrate-your-databases-to-a-fully-managed-service-with-azure-sql-database-managed-instance/).

Explorador de objetos:
- Se han incorporado opciones para no forzar los corchetes de los nombres al efectuar una acción de arrastrar y soltar del Explorador de objetos a la ventana de consulta (sugerencias de usuario [32911933](https://feedback.azure.com/forums/908035-sql-server/suggestions/32911933) y [32671051](https://feedback.azure.com/forums/908035-sql-server/suggestions/32671051)).

Clasificación de datos:
- Mejoras y correcciones de errores generales.

**Integration Services (IS)**

- Se ha agregado compatibilidad para implementar paquetes en una [Instancia administrada de SQL Database](docs/ssms/https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance).



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-tutorials-for-sql-server-management-studio-ssmstutorialstutorial-sql-server-management-studiomd"></a>2. &nbsp; [Tutoriales de SQL Server Management Studio (SSMS)](tutorials/tutorial-sql-server-management-studio.md)

*Actualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 49.  ms.author= "mathoma".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b272c75bab04912ebb706098cf6b6a6c80d9e2b8 d453ebc8251fb83ffcb1af58c9a08bb65b3e9fa2  (PR=5676  ,  Filename=tutorial-sql-server-management-studio.md  ,  Dirpath=docs\ssms\tutorials\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



- Tutorial: Conexión a SQL Server y realización de consultas con SSMS

    En este tutorial aprenderá a conectarse a su instancia de SQL Server. También aprenderá algunos comandos básicos de Transact-SQL (T-SQL) para crear y consultar una base de datos nueva.

- Tutorial: Creación de scripts de objetos en SSMS

    En este tutorial aprenderá a crear scripts de distintos objetos en SSMS, incluidas las bases de datos y las consultas.

- Tutorial: Uso de plantillas en SSMS

    En este tutorial aprenderá a trabajar con las plantillas predefinidas en SSMS. Las plantillas, una característica poco conocida, almacenan fragmentos de código Transact-SQL para diferentes tareas de administración de bases de datos.

- Tutorial: Configuración de SSMS

    En este tutorial, aprenderá los conceptos básicos de la configuración de su entorno de SSMS, como cambiar el diseño del entorno. También conocerá los diferentes componentes de SSMS.


- Tutorial: Otras recomendaciones y trucos al usar SSMS

    En este tutorial aprenderá otras recomendaciones y trucos a la hora de usar SSMS. Se incluyen las siguientes lecciones:
    - Agregar y quitar marcas de comentario del texto
    - Aplicar sangría al texto
    - Filtrar objetos en el Explorador de objetos
    - Acceder al registro de errores de SQL Server
    - Buscar el nombre de su instancia.








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

