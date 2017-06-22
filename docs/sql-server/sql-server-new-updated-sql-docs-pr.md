---
title: 'Actualizado: los documentos de SQL Server | Documentos de Microsoft'
description: "Mostrar fragmentos de contenido actualizado para recientemente modificadas en documentación, SQL Server."
services: na
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: BYHAM
ms.service: na
ms.topic: updart-autogen
ms.technology: database-engine
ms.custom: UpdArt.exe
ms.workload: sql-server
ms.tgt_pltfrm: na
ms.devlang: na
ms.date: 05/23/2017
ms.author: genemi
ms.translationtype: Human Translation
ms.sourcegitcommit: 96f6a7eeb03fdc222d0e5b42bcfbf05c25d11db6
ms.openlocfilehash: 7fba3b05943b93c0a2c0e76c2d0d5f2696a48d1c
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="new-and-recently-updated-sql-server-docs"></a>Las nuevas y recientemente actualizado: los documentos de servidor de SQL



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su [Docs.Microsoft.com](http://docs.microsoft.com/) sitio Web de documentación. Este artículo muestra extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

En este artículo es generado por un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto, o como marcado del artículo de origen. Nunca las imágenes se muestran aquí.

Actualizaciones recientes se notifican para el siguiente intervalo de fechas y el asunto:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **2017-05-01** &nbsp; - a - &nbsp; **2017-05-23**
- *Área de asunto:* &nbsp; **SQL Server**.




&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

Esta sección muestra los extractos de las actualizaciones que se recopilan de los artículos que han presentado recientemente una actualización a gran escala.

Los extractos que se muestran aquí aparecen separados de su contexto semántica correcta. Además, en ocasiones, un extracto se separa de la sintaxis de markdown importante que rodea en el artículo real. Por lo tanto, estos extractos son para obtener instrucciones generales solo. Los extractos de sólo le permiten saber si sus intereses garantizan dedicar tiempo a haga clic en y visite el artículo real.

Por estas y otras razones, no se copie el código de estos fragmentos y no toma como verdaderos exacta cualquier fragmento de texto. En su lugar, visite el artículo real.



&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-sql-server-2017-release-notessql-server-2017-release-notesmd"></a>1. &nbsp;[Notas de la versión SQL Server de 2017](sql-server-2017-release-notes.md)

*Updated: 2017-05-17* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Next](#TitleNum_2))

<!-- Source markdown line 28.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 84e7a2a49f2893d49380db1ad75695d9a4fd59b2 27a145ad30c10fd667f926d2e092b88c0ba586c5 -->



**CTP de SQL Server de 2017 2.1 (mayo de 2017)**

**Documentación (CTP 2.1)**

- **Problema e impacto:** documentación para [! INCLUDE [ssSQLv14_md--.. /includes/sssqlv14-MD.MD)] es limitado y contenido se incluye con la [! INCLUDE [ssSQL15_md--.. conjunto de documentación de /includes/sssql15-MD.MD)].  Contenido de artículos que es específico de [! INCLUDE [ssSQLv14_md--.. /includes/sssqlv14-MD.MD)] se anotará con **se aplica a**. 
- **Problema e impacto:** ningún contenido sin conexión está disponible para [! INCLUDE [ssSQLv14_md--.. /includes/sssqlv14-MD.MD)].

**SQL Server Reporting Services (CTP 2.1)**


- **Problema e impacto:** si tiene SQL Server Reporting Services y Power de servidor de informes BI en el mismo equipo y desinstalar uno de ellos, ya no podrá conectarse al servidor de informes con el Administrador de configuración del servidor de informes restantes.
- **Solución alternativa** para solucionar este problema, debe realizar las siguientes operaciones después de desinstalar uno de los servidores.

    1. Inicie un símbolo del sistema en modo de administrador.
    2. Vaya al directorio donde está instalado el servidor de informes restantes.

        *Ubicación predeterminada de servidor de informes de Power BI: servidor de informes de C:\Program Files\Microsoft Power BI*

        *Ubicación predeterminada de SQL Server Reporting Services: C:\Program Files\Microsoft SQL Server Reporting Services*

    3. A continuación, vaya a la carpeta siguiente. Esto será *SSRS* o *PBIRS* según lo que queda.
    4. Vaya a la carpeta WMI.
    5. Ejecute el siguiente comando:

        ```
        regsvr32 /i ReportingServicesWMIProvider.dll
        ```

        Puede omitir el error siguiente, si lo ve.

        ```
        The module "ReportingServicesWMIProvider.dll" was loaded but the entry-point DLLInstall was not found. Make sure that "ReportingServicesWMIProvider.dll" is a valid DLL or OCX file and then try again.
        ```

**TSqlLanguageService.msi (CTP 2.1)**


- **Problema e impacto:** después de instalar en un equipo que tenga una versión de 2016 *TSqlLanguageService.msi* (mediante el programa de instalación de SQL o como un paquete redistribuible independiente) la v13.* (SQL 2016) versiones instaladas de *Microsoft.SqlServer.Management.SqlParser.dll* y *Microsoft.SqlServer.Management.SystemMetadataProvider.dll* se quitan. Todas las aplicaciones que tienen una dependencia en las versiones de 2016 de dichos ensamblados, a continuación, dejarán de funcionar, dando a un error similar al: *error: no se pudo cargar el archivo o ensamblado ' Microsoft.SqlServer.Management.SqlParser, Version = 13.0.0.0, Culture = neutral, PublicKeyToken = 89845dcd8080cc91' o uno de sus dependencias. El sistema no encuentra el archivo especificado.*




&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-what39s-new-in-sql-server-2017what-s-new-in-sql-server-2017md"></a>2. &nbsp;[¿Qué &#39; s de SQL Server de 2017](what-s-new-in-sql-server-2017.md)

*Updated: 2017-05-22* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;  ([Previous](#TitleNum_1))

<!-- Source markdown line 31.  ms.author= "craigg".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 b3e965f62414af06d42f88497958a4bca67befce 82ad09ae9a917f26db3e2210b5cf89585e0e4c4e -->



**Novedades de CTP de SQL Server de 2017 2.1 (mayo de 2017)**

** Motor de base de datos de servidor SQL **

- Un nuevo DMF, [sys.dm_db_log_stats--.. / relational-databases/system-dynamic-management-views/sys-dm-db-log-stats-transact-sql.md), se introdujo para exponer atributos de nivel de resumen e información sobre los archivos de registro de transacciones; es útil para supervisar el estado del registro de transacciones.  
- Esta versión de CTP contiene correcciones de errores y mejoras de rendimiento para el motor de base de datos.
- Para obtener una lista detallada de 2017 mejoras CTP en versiones anteriores de CTP, consulte [What's New in SQL Server 2017 (motor de base de datos)--.. / database-engine/configure-windows/what-s-new-in-sql-server-2017-database-engine.md).

**SQL Server Reporting Services (SSRS)**

- SQL Server Reporting Services ya no está disponible para instalarse, mediante el programa de instalación de SQL Server a partir de CTP 2.1.
- Comentarios ahora están disponibles para los informes. Los comentarios permiten agregar perspectiva con lo que se encuentra en un informe y colaborar con otras personas de su organización. También puede incluir archivos adjuntos con el comentario.
- Para SSRS más detallada, ¿qué es información nueva, incluidos los detalles de las versiones anteriores, consulte [' s new en Reporting Services:.. / reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md). 
- Para obtener información sobre el servidor de informes de Power BI, consulte [empezar a trabajar con el servidor de informes de Power BI](https://powerbi.microsoft.com/documentation/reportserver-get-started/).

**Servicios de aprendizaje de máquina SQL Server**

- No hay ninguna característica de servicios de aprendizaje de máquinas nuevas en esta versión de CTP.
- Para los servicios de aprendizaje de máquina más detallada, ¿qué es información nueva, incluidos los detalles de los lanzamientos anteriores de CTP, consulte [What's New en SQL Server Machine Learning Services--.. / advanced-analytics/what-s-new-in-sql-server-machine-learning-services.md).  

**SQL Server Analysis Services (SSAS)**

- No hay características de SSAS nuevas en este CTP.  
- Para obtener más información sobre mejoras y correcciones de errores en esta versión, consulte [What's New en SQL Server de 2017 Analysis Services--.. / analysis-services/what-s-new-in-sql-server-analysis-services-2017.md).  





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Compact lista de artículos que se actualizó recientemente

Esta lista compact proporciona vínculos a todos los artículos actualizados que se enumeran en la sección anterior.

1. [Notas de la versión SQL Server de 2017](#TitleNum_1)
2. [¿Qué &#39; s de SQL Server de 2017](#TitleNum_2)


<a name="sisters2"/>

&nbsp;

## <a name="sister-articles"></a>Hermana artículos

Esta sección enumeran artículos muy similar para los artículos actualizados recientemente en otras áreas temáticas, dentro del mismo repositorio de GitHub.


&nbsp;

[Microsoft /**pr de documentos de sql** ](https://github.com/microsoftdocs/sql-docs-pr/) repositorio en GitHub.com:

- [Actualizado recientemente: **Microsoft SQL Server y bases de datos relacionales** documentos](/sql/relational-databases/relational-databases-new-updated-sql-docs-pr)
- [Actualizado recientemente: **Microsoft SQL Server** documentos](/sql/sql-server/sql-server-new-updated-sql-docs-pr)
- [Actualizado recientemente: **Transact-SQL en SQL Server** documentos](/sql/t-sql/t-sql-new-updated-sql-docs-pr)


&nbsp;

<!--
[Microsoft/**azure-docs**](https://github.com/microsoft/azure-docs/) repository on GitHub.com:

- [Sisters list for **azure-docs** repo](https://docs.microsoft.com/azure/sql-server-new-updated-azure-docs/#sisters2)
-->

&nbsp;



