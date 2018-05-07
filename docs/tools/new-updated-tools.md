---
title: 'Actualizado: Documentación de Tools for SQL Server | Microsoft Docs'
description: Muestra fragmentos de contenido actualizado de documentación modificada recientemente para Tools for Microsoft SQL Server.
manager: craigg
author: MightyPen
ms.author: genemi
ms.topic: article
ms.custom: UpdArt.exe
ms.suite: sql
ms.technology: release-landing
ms.prod: sql
ms.prod_service: sql-non-specified
ms.component: tools
ms.date: 04/28/2018
ms.openlocfilehash: 0547653c4fc2d8bd04f851b843e74fd9ec78d2ea
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MTE
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="new-and-recently-updated-tools-for-sql-server"></a>Nuevos y actualizados recientemente: Tools para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; del **03-02-2018** &nbsp; al &nbsp; **28-04-2018**
- *Área de asunto:* &nbsp; **Tools para SQL Server**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


- [herramienta de consulta de línea de comandos de cli MSSQL para SQL Server](mssql-cli.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

### <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

En esta lista compacta se proporcionan vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

- [bcp (utilidad)](#TitleNum_1)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-bcp-utilitybcp-utilitymd"></a>1. &nbsp; [bcp (utilidad)](bcp-utility.md)

*Actualizado: 25-04-2018* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; 

<!-- Source markdown line 189.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 c85e6c6ff13ad20f432ead67febfc48c784f3f9a 27de3822192fc64f0d99b4dbc21f05a3e4def186  (PR=5676  ,  Filename=bcp-utility.md  ,  Dirpath=docs\tools\  ,  MergeCommitSha40=a85a46312acf8b5a59a8a900310cf088369c4150) -->



**-G**<a name="G"></a> El cliente usa este modificador al conectarse a Azure SQL Database o Azure SQL Data Warehouse para especificar que el usuario se autentica mediante la autenticación de Azure Active Directory. Requiere el modificador -G [versión 14.0.3008.27 o posterior](http://go.microsoft.com/fwlink/?LinkID=825643). Para determinar su versión, ejecute bcp -v. Para obtener más información, consulte [Use Azure autenticación de Active Directory para la autenticación con la base de datos SQL o almacenamiento de datos de SQL](https://docs.microsoft.com/azure/sql-database/sql-database-aad-authentication).

> [!TIP]
>  Para comprobar si su versión de bcp incluye compatibilidad para el tipo de autenticación Azure Active Directory (AAD) **bcp--** (bcp\<espacio >\<guión >\<guión >) y compruebe que ve - G en la lista de argumentos disponibles.

- **Nombre de usuario y contraseña de Azure Active Directory:**

    Si desea utilizar un nombre de usuario y una contraseña de Azure Active Directory, puede proporcionar la opción **- G** y usar también el nombre de usuario y la contraseña proporcionando las opciones **- U** y **-P** .

    En el ejemplo siguiente se exporta datos con el nombre de usuario de Azure AD y la contraseña que el usuario y la contraseña es una credencial de AAD. En el ejemplo se exporta la tabla `bcptest` de base de datos `testdb` de servidor de Azure `aadserver.database.windows.net` y almacena los datos en el archivo `c:\last\data1.dat`:
```
    bcp bcptest out "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
```

    The following example imports data using Azure AD Username and Password where user and password is an AAD credential. The example imports data from file `c:\last\data1.dat` into table `bcptest` for database `testdb` on Azure server `aadserver.database.windows.net` using Azure AD User/Password:
```
    bcp bcptest in "c:\last\data1.dat" -c -t -S aadserver.database.windows.net -d testdb -G -U alice@aadtest.onmicrosoft.com -P xxxxx
```



- **Autenticación integrada de Azure Active Directory**

    Para autenticación integrada de Azure Active Directory, proporcione la opción **-G** sin un nombre de usuario o contraseña. Esta configuración da por supuesto que la cuenta de usuario de Windows actual (la cuenta que se está ejecutando el comando bcp) está federada con Azure AD:







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

