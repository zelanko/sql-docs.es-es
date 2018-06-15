---
title: 'Actualizados: documentos de SSDT para SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Data Tools (SSDT) para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssdt
ms.date: 04/28/2018
ms.openlocfilehash: 99b0844803e1ce95bd6f73b0d45a2baf867428ba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32699716"
---
# <a name="new-and-recently-updated-sql-server-data-tools-ssdt"></a>Nuevos y actualizados recientemente: SQL Server Data Tools (SSDT)



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área temática:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Compatibilidad de Azure Active Directory con SQL Server Data Tools (SSDT)](azure-active-directory.md)



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

*Actualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 29.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 de18314845cffa197b3fd2ed868f2c330760bedb 5487de1ed57c16a6517a3a8849f412c208f1889f  (PR=5676  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->





**SSDT para Visual Studio 2017 (15.6.0)**

Número de compilación: 14.0.16162.0 Fecha de lanzamiento: 10 de abril de 2018

**Novedades**


**SSIS:**

1.  Se corrige un problema por el que la tarea de procesamiento de sistema autónomo (AS) no registra ningún paso de procesamiento al establecer SQLServer2016 o SQLServer2017 como destino.
2.  Se corrige un problema por el que se produce una infracción de acceso al abrir dtsx con nombres de tareas muy largos y no escrito en inglés en SSDT.
3.  Se corrige un problema por el que, a veces, la lista de variables de ScriptTask desaparece de la interfaz de usuario de la tarea.
4.  Se corrige un problema por el que se genera un error al agregar una copia del paquete existente si la ubicación del paquete es SQL Server.
5.  Se corrige un problema por el que el foco se bloquea al acceder al cuadro combinado en algunos cuadros de diálogo del editor.
6.  Se corrige un problema por el que el fondo no cambia junto al tema de VS.
7.  Se corrige un problema por el que la etiqueta de anotación y carga es invisible en el tema oscuro.
8.  Se corrige un problema por el que la propiedad de estado no se define correctamente para los elementos eliminados del cuadro de herramientas de SSIS.
9.  Se corrige un problema por el que nunca se puede ejecutar WebServiceTask.
10. Se corrige un problema por el que la implementación del paquete genera un error si la cadena de conexión está establecida como variable con una expresión que depende de los parámetros del proyecto.

**Instalador:**

1.  Se agrega el vínculo "Programa para la mejora de la experiencia del usuario de SQL Server Data Tools" en el aviso de privacidad.
2.  Se corrige un problema por el que la ventana instalador de Visual Studio aparece como elemento emergente al seleccionar la opción "Instalar la nueva instancia de SQL Server Data Tools para Visual Studio 2017".

**Problemas conocidos:**

1.  La tarea Ejecutar paquete de SSIS no admite la depuración cuando ExecuteOutofProcess está establecido en True. Este problema solo se aplica a la depuración. Las funciones de guardado, implementación y ejecución mediante DTExec.exe o el catálogo de SSIS no se verán afectadas.



**SSDT para Visual Studio 2017 (15.5.2)**

Número de compilación: 14.0.16156.0

**Novedades**


**SSIS**
1.  Se corrige un problema por el que la migración de proyectos de SSIS 2008 genera un error si SSAS y SSIS están instalados en la misma instancia de VS 2017.
2.  Se corrige un problema que impide que los proyectos de Rdlc se compilen cuando el diseñador de informes Rdlc y SSIS están instalados en la misma instancia de VS 2017.







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

