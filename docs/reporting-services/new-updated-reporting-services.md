---
title: 'Actualización: Documentos de Reporting Services para SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente para Reporting Services para Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: ssrs
ms.date: 04/28/2018
ms.openlocfilehash: 5fc0153c45e12f8cef47ef2b9eef10f73343b87e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32673735"
---
# <a name="new-and-recently-updated-reporting-services-for-sql-server"></a>Nuevo y actualizado recientemente: Reporting Services para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área de asunto:* &nbsp; **Reporting Services para SQL Server**.




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

1. [Registro de cambios de SQL Server Reporting Services](#TitleNum_1)
2. [Implementar el elemento web Visor de informes de SQL Server Reporting Services en un sitio de SharePoint](#TitleNum_2)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-change-log-for-sql-server-reporting-serviceschange-log-sql-server-reporting-servicesmd"></a>1. &nbsp; [Registro de cambios de SQL Server Reporting Services](change-log-sql-server-reporting-services.md)

*Actualizado: 27-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "edugonz".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 025d58c01310215df423e7c3848e929b935bcfff 89310524b904dfba41e301cf1323b9a2a5e05064  (PR=575  ,  Filename=change-log-sql-server-reporting-services.md  ,  Dirpath=docs\reporting-services\  ,  MergeCommitSha40=98b04e2388872d1c7b8d819438c150c4ff2df94c) -->




- *Versión 14.0.600.744, publicada el 25 de abril de 2018*
    - Correcciones de errores:
        - La página Suscripción controlada por datos no muestra la opción de entrega una vez creada.
        - La actualización de SSRS 2012 a SSRS 2017 tiene como resultado que RSManagement lanza una excepción cada pocos segundos.
        - No se pueden modificar los valores predeterminados para parámetros de varios valores en IE11.
        - Los horarios están vacíos cada vez que se ejecuta una programación compartida.

- *Versión 14.0.600.689, publicada el 28 de febrero de 2018*
    - Correcciones de errores:
        - La visibilidad del parámetro de informe de un informe vinculado se revierte después de editar sus propiedades
        - El parámetro de la dirección URL rc:Toolbar=false no funciona en Express Edition
        - Las expresiones en TextBox con la propiedad CanGrow establecida en false hace que no se muestren los valores
        - Se agregó el vínculo "Más información" para la clave de producto en la configuración
        - El portal web con autenticación de formularios personalizados omite el deslizamiento de la cookie de expiración
        - Exportar a Word crea un alto de fila desigual si el contenido de la fila está vacío



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-deploy-the-sql-server-reporting-services-report-viewer-web-part-on-a-sharepoint-sitereport-server-sharepointdeploy-report-viewer-web-partmd"></a>2. &nbsp; [Implementar el elemento web Visor de informes de SQL Server Reporting Services en un sitio de SharePoint](report-server-sharepoint/deploy-report-viewer-web-part.md)

*Actualizado: 10-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1))

<!-- Source markdown line 154.  ms.author= "maghan".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 42b763a610d378a7cedc9b5778bc5048d65fa730 ce7e2619689fd50be51a2689b07e3137470d9adf  (PR=5481  ,  Filename=deploy-report-viewer-web-part.md  ,  Dirpath=docs\reporting-services\report-server-sharepoint\  ,  MergeCommitSha40=31e0b2ebfc08c0b57870ac412fbd49bf3a1dffb8) -->



**Solucionar problemas**


* Error al desinstalar SSRS si ha configurado el modo integrado de SharePoint:

    Install-SPRSService: [A] No se puede convertir Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService en [B]Microsoft.ReportingServices.SharePoint.SharedService.Service.ReportingWebService. El tipo A se origina a partir de"Microsoft.ReportingServices.SharePoint.SharedService,Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" en el contexto "Default" en la ubicación "C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll". El tipo B se origina a partir de"Microsoft.ReportingServices.SharePoint.SharedService,Version=12.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" en el contexto "Default" en la ubicación "C:\Windows\assembly\GAC_MSIL\Microsoft.Reporting Services.SharePoint.SharedService.dll".

    Solución:
    1. Eliminar el elemento web Visor de informes
    2. Desinstalar SSRS
    3. Volver a instalar el elemento web Visor de informes

* Error al intentar actualizar SharePointsi ha configurado el modo integrado de SharePoint:

    "No se puede cargar el archivo o ensamblado "Microsoft.ReportingServices.Alerting.ServiceContract, Version=14.0.0.0, Culture=neutral, PublicKeyToken=89845dcd8080cc91" o una de sus dependencias. El sistema no encuentra el archivo especificado. 00000000-0000-0000-0000-000000000000

    Solución:
    1. Eliminar el elemento web Visor de informes
    2. Desinstalar SSRS
    3. Volver a instalar el elemento web Visor de informes







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

