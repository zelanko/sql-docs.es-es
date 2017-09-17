---
title: "Actualizar - SSMA para la documentación de SQL Server | Documentos de Microsoft"
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, para SQL Server Migration Assistant (SSMA) para Microsoft SQL Server."
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
ms.workload: ssma-sql-server-migration-assistant
ms.translationtype: MT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 68df82bc7da6d7ef5aed3522c06704fb92bb0982
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-migration-assistant-ssma"></a>Nuevos y actualizados recientemente: SQL Server Migration Assistant (SSMA)



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-07-18** &nbsp; - a - &nbsp; **2017-09-11**
- *Área de asunto:* &nbsp; **SQL Server Migration Assistant**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


***En este momento no hay ningún artículo nuevo en la lista.***



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que se han producido recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección de citas.

1. [¿Qué &#39; s de SSMA para DB2 (DB2ToSQL)](#TitleNum_1)
2. [SQL Server Migration Assistant](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-what39s-new-in-ssma-for-db2-db2tosqldb2what-s-new-in-ssma-for-db2-db2tosqlmd"></a>1. &nbsp;[¿Qué &#39; s de SSMA para DB2 (DB2ToSQL)](db2/what-s-new-in-ssma-for-db2-db2tosql.md)

*Actualizado: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([siguiente](#TitleNum_2))

<!-- Source markdown line 24.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c5dfb378ac578f54935a8a1fa7194398f3631017 f4427d1857894ad348cef5c92fbf6b51d00ee652  (PR=3070  ,  Filename=what-s-new-in-ssma-for-db2-db2tosql.md  ,  Dirpath=docs\ssma\db2\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**SSMA v7.4**

La versión v7.4 de SSMA para DB2 contiene los siguientes cambios:
- El **tiempo de espera de consulta** opción ahora está disponible durante la detección de objetos de esquema en el origen y de destino.
! [opción de tiempo de espera de consulta--.. /Media/Query-timeout_red.png)

- La métrica de calidad y la conversión se ha mejorado con correcciones de destino, en función de los comentarios de clientes.

> [!IMPORTANT]
> .NET 4.5.2 es un requisito previo para la instalación de SSMA v7.4. Además, a partir de v7.4, la versión de 32 bits de SSMA se está suspendida.

**SSMA v7.3**

La versión v7.3 de SSMA para DB2 contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Marco de extensibilidad SSMA expuesta a través de los siguientes elementos:
  - Funcionalidad de exportación a un proyecto de SQL Server Data Tools (SSDT).
    -   Ahora puede exportar las secuencias de comandos de esquema de SSMA para un proyecto de SSDT. Puede utilizar las secuencias de comandos de esquema para realizar cambios de esquema adicionales e implementar la base de datos.
! [Guardar como comando de proyecto SSDT--... /Media/Export-Schema-scripts_red.png)
  - Bibliotecas que pueden utilizarse SSMA para realizar conversiones personalizadas.
    - Ahora puede construir código que puede controlar las conversiones de sintaxis personalizados y las conversiones que antes no estaban realizaba SSMA.
      - Las instrucciones sobre cómo construir un convertidor personalizado están disponibles en esta entrada de blog, [funciones de conversión del ampliación de SQL Server Migration Assistant](https://blogs.msdn.microsoft.com/datamigration/2017/02/21/2185/).
      - Proyecto de ejemplo para la conversión se puede descargar este [entrada de blog](https://blogs.msdn.microsoft.com/datamigration/ssmafororacleconversionsample/).

**SSMA v7.2**

La versión de v7.2 de SSMA para DB2 contiene los siguientes cambios:
- Métrica de calidad y la conversión mejorada con correcciones de destino en función de los comentarios de clientes.
- Mejoras de telemetría para proporcionar una mejor puntos de datos para solucionar problemas de los clientes y mejorar las tasas de conversión de SSMA.



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-sql-server-migration-assistantsql-server-migration-assistantmd"></a>2. &nbsp;[SQL Server Migration Assistant](sql-server-migration-assistant.md)

*Actualizado: 2017-09-07* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_1))

<!-- Source markdown line 36.  ms.author= "Shamikg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 340d718e85fa73c6722862a0a7ba90239b247389 b29f4be2b6d208fd6038c2f9e1c7f0b7bd6b9ed7  (PR=3070  ,  Filename=sql-server-migration-assistant.md  ,  Dirpath=docs\ssma\  ,  MergeCommitSha40=0b832a9306244210e693bde7c476269455e9b6d8) -->



**Orígenes compatibles y las versiones de destino**

Para los orígenes admitidos, revise la información en el centro de descarga para la descarga SSMA.

Se admiten las siguientes versiones de destino de SSMA.

- SQL Server 2008
- SQL Server 2008 R2
- SQL Server 2012
- SQL Server 2014
- SQL Server 2016
- Base de datos SQL de Azure
- SQL Server de 2017 en Windows y Linux (versión preliminar)
- ** Almacenamiento de datos azure SQL

** Este destino solo es compatible con SSMA para Oracle.









## <a name="similar-articles"></a>Artículos similares

<!--  HOW TO:
    Refresh this file's line items with the latest 'Count-in-Similars*' content.
    Then run Run-533-*.BAT
-->

En esta sección se enumera los artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro de nuestro repositorio público de GitHub.com: [MicrosoftDocs/sql-docs](https://github.com/MicrosoftDocs/sql-docs/).

#### <a name="subject-areas-which-do-have-new-or-recently-updated-articles"></a>Áreas temáticas con artículos nuevos o actualizados recientemente

- [Nuevos y actualizados (3 + 12): **Advanced Analytics para SQL** documentos](../advanced-analytics/new-updated-advanced-analytics.md)
- [Nuevos y actualizados (5 + 0): **conectar con SQL Server** documentos](../connect/new-updated-connect.md)
- [Nuevos y actualizados (5 + 1): **motor de base de datos de SQL** documentos](../database-engine/new-updated-database-engine.md)
- [Nuevos y actualizados (19 + 82): **Integration Services para SQL** documentos](../integration-services/new-updated-integration-services.md)
- [Nuevos y actualizados (1 + 8): **Linux para SQL** documentos](../linux/new-updated-linux.md)
- [Nuevos y actualizados (12 + 1): **bases de datos relacionales de SQL** documentos](../relational-databases/new-updated-relational-databases.md)
- [Nuevos y actualizados (0 + 1): **Reporting Services para SQL** documentos](../reporting-services/new-updated-reporting-services.md)
- [Nuevos y actualizados (7 + 1): **Microsoft SQL Server** documentos](../sql-server/new-updated-sql-server.md)
- [Nuevos y actualizados (1 + 1): **SQL Server Data Tools (SSDT)** documentos](../ssdt/new-updated-ssdt.md)
- [Nuevos y actualizados (0 + 2): **SQL Server Migration Assistant (SSMA)** documentos](../ssma/new-updated-ssma.md)
- [Nuevos y actualizados (1 + 4): **SQL Server Management Studio (SSMS)** documentos](../ssms/new-updated-ssms.md)
- [Nuevos y actualizados (4 + 1): **Transact-SQL** documentos](../t-sql/new-updated-t-sql.md)
- [Nuevos y actualizados (0 + 1): **Tools para SQL** documentos](../tools/new-updated-tools.md)

#### <a name="subject-areas-which-have-no-new-or-recently-updated-articles"></a>Áreas temáticas sin artículos nuevos ni actualizados recientemente

- [Nuevos + Actualizados (0+0): documentos de **Objetos de datos ActiveX (ADO) para SQL**](../ado/new-updated-ado.md)
- [Nuevos y actualizados (0 + 0): **Analysis Services para SQL** documentos](../analysis-services/new-updated-analysis-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Data Quality Services para SQL**](../data-quality-services/new-updated-data-quality-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Extensiones de minería de datos (DMX) para SQL**](../dmx/new-updated-dmx.md)
- [Nuevos y actualizados (0 + 0): **Master Data Services (MDS) para SQL** documentos](../master-data-services/new-updated-master-data-services.md)
- [Nuevos + Actualizados (0+0): documentos de **Expresiones multidimensionales (MDX) para SQL**](../mdx/new-updated-mdx.md)
- [Nuevos + Actualizados (0+0): documentos de **ODBC (conectividad abierta de bases de datos) para SQL**](../odbc/new-updated-odbc.md)
- [Nuevos + Actualizados (0+0): documentos de **PowerShell para SQL**](../powershell/new-updated-powershell.md)
- [Nuevos + Actualizados (0+0): documentos de **Ejemplos para SQL**](../sample/new-updated-sample.md)
- [Nuevos + Actualizados (0+0): documentos de **XQuery para SQL**](../xquery/new-updated-xquery.md)



