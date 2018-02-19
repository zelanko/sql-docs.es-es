---
title: 'Actualizados: documentos de SSDT para SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Data Tools (SSDT) para Microsoft SQL Server."
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 02/03/2018
ms.openlocfilehash: c591ddddd60af31fe2d338fdee25ea2c17ab0ea5
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Nuevos y actualizados recientemente: SQL Server Data Tools (SSDT)



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-12-2017** &nbsp; al &nbsp; **03-02-2018**
- *Área temática:* &nbsp; **SQL Server Data Tools (SSDT)**.




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

1. [Registro de cambios para SQL Server Data Tools (SSDT)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd"></a>1. &nbsp; [Registro de cambios para SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Actualizado: 18-01-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 28.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 6416949beaee91da2f77dfebb9eb5ed363db4cb7 de18314845cffa197b3fd2ed868f2c330760bedb  (PR=4652  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=6b4aae3706247ce9b311682774b13ac067f60a79) -->



**SSDT para Visual Studio 2017 (15.5.1)**

Número de compilación: 14.0.16148.0

**Novedades**


Visual Studio 2017 (15.5.1) es la misma versión que la 15.5.0 excepto por las siguientes correcciones de errores del instalador:

1.  Se ha corregido un problema que provocaba que el instalador se bloquease en el proceso posterior a la instalación de SQL Server Integration Services.
2.  Se ha corregido un problema que provocaba un error en la instalación con el siguiente mensaje de error: "La operación de metarchivo solicitada no es compatible (0x800707D3)".

Además de estas dos correcciones de errores, todavía se aplican los siguientes detalles de la versión 15.5.0 a la versión 15.5.1.

**SSDT para Visual Studio 2017 (15.5.0)**

Número de compilación: 14.0.16146.0

**Novedades**


SSDT para Visual Studio 2017 (15.5.0) deja de estar en versión preliminar y pasa a disponibilidad general (GA).

**Instalador**
1. La interfaz de usuario del programa de instalación está localizada.
1. Se reemplaza el icono con uno de mayor calidad.

**Integration Services (IS)**
1. Se ha agregado el paso de validación de paquetes en el Asistente para implementación al implementar Azure SSIS IR en ADF, con el que se pueden detectar potenciales errores de compatibilidad en paquetes de SSIS cuando se ejecutan en Azure SSIS IR. Para obtener más información, vea [Validación de paquetes de SSIS implementados en Azure](..\integration-services\lift-shift\ssis-azure-validate-packages.md).
1. Se ha localizado la extensión SSIS.

**Correcciones de errores**


**Integration Services (IS)**
1. Se ha corregido un problema que provocaba que el diseño del administrador de conexiones de OLEDB y ADO.NET estuviese dañado.
2. Se ha corregido un problema que provocaba un error de ensamblado no encontrado al intentar editar una tarea de procesamiento de dimensiones.

**Problemas conocidos**


La tarea Ejecutar paquete de **Integration Services (IS)** SSIS no admite la depuración cuando ExecuteOutofProcess está establecido en True. Este problema solo se aplica a la depuración. Las funciones de guardado, implementación y ejecución mediante DTExec.exe o el catálogo de SSIS no se verán afectadas.



**SSDT 17.4 para Visual Studio 2015**

Número de compilación: 14.0.61712.050

**Novedades**


**Proyectos de Analysis Services (AS)**
- Se han agregado tres opciones nuevas a los proyectos tabulares (en Opciones > Tabular de Analysis Services > Importación de datos):







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
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + actualizados (0+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


