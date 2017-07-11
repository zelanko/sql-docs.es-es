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
ms.date: 06/30/2017
ms.author: genemi
ms.workload: ssdt-sql-server-data-tools
ms.translationtype: Human Translation
ms.sourcegitcommit: dcf26be9dc2e502b2d01f5d05bcb005fd7938017
ms.openlocfilehash: 5e43cb76dac922b3c43318b2a9f539ab19ec7bfe
ms.contentlocale: es-es
ms.lasthandoff: 07/03/2017

---
<a id="new-and-recently-updated-sql-server-data-tools-ssdt" class="xliff"></a>

# Nuevos y actualizados recientemente: SQL Server Data Tools (SSDT)



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **17-05-2017** &nbsp; a &nbsp; **30-06-2017**
- *Área temática:* &nbsp; **SQL Server Data Tools (SSDT)**.




&nbsp;

<a id="new-articles-created-recently" class="xliff"></a>

## Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


*En este momento no hay ningún artículo nuevo en la lista.*



&nbsp;

<a id="updated-articles-with-excerpts" class="xliff"></a>

## Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que han presentado recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

<a id="1-nbsp-changelog-for-sql-server-data-tools-ssdtchangelog-for-sql-server-data-tools-ssdtmd" class="xliff"></a>

### 1. &nbsp; [Registro de cambios para SQL Server Data Tools (SSDT)](changelog-for-sql-server-data-tools-ssdt.md)

*Actualizado: 19-05-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 21.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cf17883ce0daf75fdf88881171bf4042558b1cf4 536fe0fe41b023a4186f494a509fa14fcbafccf4  (PR=1777  ,  Filename=changelog-for-sql-server-data-tools-ssdt.md  ,  Dirpath=docs\ssdt\  ,  MergeCommitSha40=5bd0e1d3955d898824d285d28979089e2de6f322) -->



Para ver entradas detalladas sobre las novedades y los cambios, visite [el blog del equipo de SSDT](https://blogs.msdn.microsoft.com/ssdt/)

**SSDT 17.1**

Número de compilación: 14.0.61705.170

**Novedades**

**Proyectos de AS:**
- Los usuarios pueden establecer codificación sugerencias en columnas de la interfaz de usuario en los modelos de 1400
- IntelliSense relacionado con el modelo no estará disponible en modo sin conexión
- Explorador de modelos tabulares ahora contiene un nodo para representar expresiones de M con nombre disponibles en el modelo (modelos tabulares de nivel de compatibilidad de 1400)
- Azure Active Directory selector de personas similar a IAM del Portal de Microsoft Azure ya está disponible al configurar los miembros del rol en los modelos tabulares

**Proyectos de base de datos:**
- Actualiza a DacFx 17.1

**Correcciones de errores**

- Se corrigió un problema donde se muestra incorrectamente el nombre del grupo de diseñadores de Business Intelligence en las opciones de Visual Studio en VS2017
- Se corrigió un problema que puede producirse un bloqueo de generar un mapa de código para una solución con un proyecto de informe o como proyecto
- Se ha corregido una serie de problemas con la integración de PowerQuery para modelos tabulares de nivel de compatibilidad de Analysis Services 1400
- Ventana de herramientas, donde el operador de asignación no podría encontrarse en una línea independiente al definir una medida se corrigió un problema en el nuevo editor de DAX
- Se corrigió un problema que impide que la presentación tabular medida actualizar al cambiar el nombre de las medidas de perspectiva
- Implementar actualizada motor del área de trabajo integrado de Analysis Services y modelo de objetos tabulares que corrige una regresión que provocó que contiene traducciones produce un error en los proyectos tabulares 1200 en servidor SQL Server 2016 Analysis Services
- Corregido un problema de rendimiento que realiza creation\deletion de nuevos orígenes de datos tabulares de 1400 muy lento
- Se corrigió un problema en el diagrama de la DSV en modelos multidimensionales podría detener representación si cambiar la vista rápidamente entre diferentes DSV

**DacFx 17.1**

- Se ha corregido un problema al cifrar una columna con tablas optimizadas en memoria con otras columnas de identidad
- Compatibilidad con SQLDOM opción CATALOG_COLLATION para crear la base de datos





&nbsp;

<a name="compactupdatedlist"/>

<a id="compact-list-of-articles-updated-recently" class="xliff"></a>

## Compact lista de artículos que se actualizó recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección anterior.

1. [Registro de cambios para SQL Server Data Tools (SSDT)](#TitleNum_1)




<a name="sisters2"/>

&nbsp;

<a id="sister-articles" class="xliff"></a>

## Hermana artículos

En esta sección se enumeran artículos muy similares a los artículos actualizados recientemente en otras áreas temáticas, dentro del mismo repositorio de GitHub.com: [MicrosoftDocs/**sql-docs-pr**](https://github.com/microsoftdocs/sql-docs-pr/).

<!--  20170630-1150  -->

<a id="subject-areas-which-do-have-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos + Actualizados (12+2): documentos de **Análisis avanzado para SQL**](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos + Actualizados (1+0): documentos de **Analysis Services para SQL**](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+2): documentos de **Conectar con SQL**](../connect/new-updated-connect.md)
- [Nuevos + Actualizados (3+0): documentos de **Motor de base de datos para SQL**](../database-engine/new-updated-database-engine.md)
- [Nuevos + Actualizados (1+2): documentos de **Integration Services para SQL**](../integration-services/new-updated-integration-services.md)
- [Nuevos + Actualizados (2+8): documentos de **Linux para SQL**](../linux/new-updated-linux.md)
- [Nuevos + Actualizados (1+0): documentos de **Master Data Services (MDS) para SQL**](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (5+5): documentos de **Bases de datos relacionales para SQL**](../relational-databases/new-updated-relational-databases.md)
- [Nuevos + Actualizados (2+0): documentos de **Reporting Services para SQL**](../reporting-services/new-updated-reporting-services.md)
- [Nuevos + Actualizados (0+4): documentos de **Microsoft SQL Server**](../sql-server/new-updated-sql-server.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Data Tools (SSDT)**](../ssdt/new-updated-ssdt.md)
- [Nuevos + Actualizados (0+1): documentos de **SQL Server Management Studio (SSMS)**](../ssms/new-updated-ssms.md)
- [Nuevos + Actualizados (1+0): documentos de **Herramientas para SQL**](../tools/new-updated-tools.md)


<a id="subject-areas-which-have-no-new-or-recently-updated-articles" class="xliff"></a>

#### Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **SQL Server Migration Assistant (SSMA)**](../ssma/new-updated-ssma.md)
- [Nuevos + Actualizados (0+0): documentos de **Transact-SQL**](../t-sql/new-updated-t-sql.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)


&nbsp;


