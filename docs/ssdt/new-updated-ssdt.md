---
title: 'Actualizados: documentos de SSDT para SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Data Tools (SSDT) para Microsoft SQL Server."
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
ms.date: 09/11/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 8ae9a49443525524cf7f6ffceba4fb44984c7052
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Nuevos y actualizados recientemente: SQL Server Data Tools (SSDT)



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **18-07-2017** &nbsp; a &nbsp; **11-09-2017**
- *Área temática:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Términos de licencia de SQL Server Data Tools](sql-server-data-tools-license-terms-vs2017.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compacta proporciona vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Registro de cambios para SQL Server Data Tools (SSDT)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Registro de cambios para SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Actualizado: 23-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 23.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 536fe0fe41b023a4186f494a509fa14fcbafccf4 e5bc7b76c1755f5a1af77f6cd63d8e8691dafe7b  (PR=2927  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=71a2cbf181c94c4c1aff877614aadf890b2496e0) -->



**SSDT para Visual Studio 2017 (versión preliminar 15.3.0)**

Número de compilación: 14.0.16121.0

**Novedades**


Esta versión preliminar es la primera versión de SSDT para Visual Studio 2017. Presenta una experiencia de instalación web independiente para los proyectos de SQL Server Database, Analysis Services, Reporting Services e Integration Services en Visual Studio 2017 15.3 y versiones posteriores.


**Problemas conocidos**

- El instalador no está localizado.
- SSIS no está localizado.
- La tarea Ejecutar paquete de SSIS no admite la depuración cuando *ExecuteOutofProcess* está establecido en *True*. Este problema solo se aplica a la depuración. Las funciones de guardado, implementación y ejecución mediante DTExec.exe o el catálogo de SSIS no se verán afectadas.
- Para obtener una lista completa de cambios, consulte el [registro de cambios--changelog-for-sql-server-data-tools-ssdt.md).
- Notifique problemas en el sitio de [comentarios de Connect sobre SSDT](https://connect.microsoft.com/SQLServer/Feedback).
- Los paquetes de SSIS que contengan extensiones de terceros no se pueden modificar para que tengan como objetivo otras versiones de servidor.


**SSDT 17.2 para Visual Studio 2015**

Número de compilación: 14.0.61707.300

**Novedades**



**Proyectos de AS:**
- Ahora puede configurarse la seguridad de nivel de objeto en el cuadro de diálogo *Roles* de seguridad avanzada en modelos tabulares de nivel de compatibilidad 1400.
- Nueva selección de miembros del rol de AAD para usuarios sin direcciones de correo electrónico en modelos de Azure AS en proyectos de AS de SSDT para VS2017.
- Nueva propiedad de proyecto "Preguntar siempre" en proyectos tabulares de AS de SSDT para personalizar el comportamiento del almacenamiento en caché de credenciales de ADAL.


**Correcciones de errores**


**General**
- Se han actualizado las referencias de personalización de marca de SQL Server 2017.

**Proyectos de AS**
- Se han realizado correcciones de rendimiento significativas para mejorar la experiencia al confirmar los cambios de medida DAX y otras modificaciones de modelo.
- Se ha corregido una serie de problemas con la integración de Power Query en proyectos de Analysis Services que usan modelos tabulares de nivel de compatibilidad 1400.
- Se ha corregido un problema solo en los proyectos multidimensionales en VS2017 en que era posible que el Diseñador de agregaciones de diseño no se pudiera cargar.







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



