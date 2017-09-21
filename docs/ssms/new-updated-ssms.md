---
title: 'Actualizados: documentos de SSMS para SQL Server | Microsoft Docs'
description: "Muestra fragmentos de contenido actualizado de documentación modificada recientemente de SQL Server Management Studio (SSMS) para Microsoft SQL Server."
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
ms.workload: ssms-sql-server-management-studio
ms.translationtype: HT
ms.sourcegitcommit: 15080827744c19120a8474f3142004c4af7a4064
ms.openlocfilehash: 917198902baf85f2bae57c9ade9f8d3e29dea357
ms.contentlocale: es-es
ms.lasthandoff: 09/13/2017

---
# <a name="new-and-recently-updated-sql-server-management-studio-ssms-for-sql-server"></a>Nuevos y actualizados recientemente: SQL Server Management Studio (SSMS) para SQL Server



Casi todos los días, Microsoft actualiza algunos de los artículos existentes en su sitio web de documentación [Docs.Microsoft.com](http://docs.microsoft.com/). En este artículo se muestran los extractos de los artículos actualizados recientemente. También pueden aparecer vínculos a artículos nuevos.

Este artículo se genera mediante un programa que se vuelve a ejecutar periódicamente. En ocasiones, un extracto puede aparecer con formato imperfecto o como recorte del artículo de origen. Aquí nunca se muestran las imágenes.

Se informa de las actualizaciones recientes del siguiente intervalo de fechas y tema:



- *Intervalo de fechas de las actualizaciones:* &nbsp; **18-07-2017** &nbsp; a &nbsp; **11-09-2017**
- *Área temática:* &nbsp; **SQL Server Management Studio (SSMS)**.




&nbsp;

## <a name="new-articles-created-recently"></a>Nuevos artículos creados recientemente

Los siguientes vínculos llevan a nuevos artículos que se han agregado recientemente.


1. [Ventana de salida de SQL Server Management Studio](output-window.md)



&nbsp;

## <a name="updated-articles-with-excerpts"></a>Artículos actualizados con extractos

En esta sección se muestran extractos de actualizaciones recopiladas de artículos que han sufrido una actualización importante recientemente.

Los extractos que se muestran aquí aparecen separados de su contexto semántico correcto. Además, en ocasiones, un extracto se separa de sintaxis de Markdown importante que lo rodea en el artículo real. Por tanto, estos extractos solo sirven de guía general. Los extractos solo le permiten saber si le interesa dedicar tiempo a hacer clic en el artículo real para visitarlo.

Por estas y otras razones, no copie código de estos fragmentos y no tome como verdad exacta ningún extracto de texto. En su lugar, visite el artículo real.





&nbsp;

<a name="compactupdatedlist"/>

## <a name="compact-list-of-articles-updated-recently"></a>Lista compacta de artículos que se han actualizado recientemente

Esta lista compacta proporciona vínculos a todos los artículos actualizados que aparecen en la sección de extractos.

1. [Descarga de SQL Server Management Studio (SSMS)](#TitleNum_1)
2. [Conexión a SQL Server o Azure SQL Database](#TitleNum_2)
3. [SQL Server Management Studio - Changelog (SSMS)](#TitleNum_3)
4. [Creación y actualización de tablas de bases de datos](#TitleNum_4)




&nbsp;

&nbsp;

<a name="TitleNum_1"/>

### <a name="1-nbsp-download-sql-server-management-studio-ssmsdownload-sql-server-management-studio-ssmsmd"></a>1. &nbsp; [Descarga de SQL Server Management Studio (SSMS)](download-sql-server-management-studio-ssms.md)

*Actualizado: 07-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Siguiente](#TitleNum_2))

<!-- Source markdown line 63.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 23260f301f86651061b47065bee43d42c92a7be4 0c2178d96b621b96bfcd2fbb782f24792debb407  (PR=2775  ,  Filename=download-sql-server-management-studio-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



SSMS 17.2 es la versión más reciente de SQL Server Management Studio. La generación 17.x de SSMS proporciona compatibilidad con casi todas las áreas de características de SQL Server 2008 a SQL Server 2017. La versión 17.x también es compatible con PaaS de SQL Analysis Services.

La versión 17.2 incluye:

- Multi-Factor Authentication (MFA)
  - Autenticación de Azure AD de varios usuarios para la autenticación universal con Multi-Factor Authentication (UA con MFA)
  - Se ha agregado un nuevo campo de entrada de credenciales de usuario para la autenticación universal con MFA a fin de permitir la autenticación de varios usuarios.
- El cuadro de diálogo de conexión ahora admite los siguientes cinco métodos de autenticación:
  - Autenticación de Windows
  - Autenticación de SQL Server
  - Active Directory: Universal compatible con MFA
  - Active Directory: Contraseña
  - Active Directory: Integrado

- El asistente para importación y exportación de bases de datos para DacFx ahora puede usar la autenticación universal con MFA.
- Para obtener información sobre la compatibilidad de API, consulte [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx) (Interfaz IUniversalAuthProvider).
- La biblioteca administrada de ADAL que usa la autenticación universal de Azure AD con MFA se ha actualizado a la versión 3.13.9.
- Una nueva interfaz de CLI compatible con la configuración de administración de Azure AD para SQL Database y SQL Data Warehouse.

 Para obtener más información sobre los métodos de autenticación de Active Directory, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) y [Configurar Multi-Factor Authentication de Azure SQL Database para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- La ventana de salida tiene entradas para las consultas que se ejecutan durante la expansión de los nodos del Explorador de objetos.
- Diseñador de vistas habilitado para instancias de Azure SQL Database
- Han cambiado las opciones de scripting predeterminadas para incluir en script objetos desde el Explorador de objetos en SSMS:



&nbsp;

&nbsp;

---

<a name="TitleNum_2"/>

### <a name="2-nbsp-connect-to-a-sql-server-or-azure-sql-databaseobjectconnect-to-an-instance-from-object-explorermd"></a>2. &nbsp; [Conexión a SQL Server o Azure SQL Database](object/connect-to-an-instance-from-object-explorer.md)

*Actualizado: 25-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_1) | [Siguiente](#TitleNum_3))

<!-- Source markdown line 40.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 cfd72893c35c87df96dc8605807e542be28936e2 840981d3a115a15774a8e47ee2f6a0e5c4177b01  (PR=2961  ,  Filename=connect-to-an-instance-from-object-explorer.md  ,  Dirpath=docs\ssms\object\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



   ![firewall--../media/connect-to-server/new-firewall-rule.png)

1. Para crear la regla de firewall y conectarse al servidor, haga clic en **Aceptar**.

1. El servidor se mostrará en el **Explorador de objetos** después de conectarse correctamente:

   ![connected--../media/connect-to-server/connected.png)

**Pasos siguientes**


[Creación y actualización de tablas--../visual-db-tools/design-tables-visual-database-tools.md)

**Vea también**


[SQL Server Management Studio (SSMS)--../sql-server-management-studio-ssms.md) [Descarga de SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)

[Analysis Services](https://docs.microsoft.com/sql/analysis-services/instances/connect-to-analysis-services)
[Integration Services](https://docs.microsoft.com/sql/integration-services/sql-server-integration-services)
[Reporting Services](https://docs.microsoft.com/sql/reporting-services/tools/connect-to-a-report-server-in-management-studio)



&nbsp;

&nbsp;

---

<a name="TitleNum_3"/>

### <a name="3-nbsp-sql-server-management-studio---changelog-ssmssql-server-management-studio-changelog-ssmsmd"></a>3. &nbsp; [SQL Server Management Studio - Changelog (SSMS) (SQL Server Management Studio: registro de cambios (SSMS))](sql-server-management-studio-changelog-ssms.md)

*Actualizado: 07-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([Anterior](#TitleNum_2) | [Siguiente](#TitleNum_4))

<!-- Source markdown line 20.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 1733ce3c556db1e51cb27bf830429f2c42e8f97e 2abb24fd6547e438181039d095cbad027473a57e  (PR=2775  ,  Filename=sql-server-management-studio-changelog-ssms.md  ,  Dirpath=docs\ssms\  ,  MergeCommitSha40=3f12671ace99d5fefc199c7b1c2db31e5b3cfade) -->



En este artículo, se proporcionan detalles sobre las actualizaciones, mejoras y correcciones de errores de las versiones actuales y anteriores de SSMS. Descargue las [versiones anteriores de SSMS a continuación#previous-ssms-releases).

**[SSMS 17.2--download-sql-server-management-studio-ssms.md)**


Disponible con carácter general | Número de compilación: 14.0.17177.0

**Mejoras**


- Multi-Factor Authentication (MFA)
  - Autenticación de Azure AD de varios usuarios para la autenticación universal con Multi-Factor Authentication (UA con MFA).
  - Se ha agregado un nuevo campo de entrada de credenciales de usuario para la autenticación universal con MFA a fin de permitir la autenticación de varios usuarios.
- El cuadro de diálogo de conexión ahora admite los siguientes cinco métodos de autenticación:
  - Autenticación de Windows
  - Autenticación de SQL Server
  - Active Directory: Universal compatible con MFA
  - Active Directory: Contraseña
  - Active Directory: Integrado

- El asistente para exportación e importación de bases de datos para DacFx usa la autenticación universal con MFA.
- Para obtener información sobre la compatibilidad de API, consulte [IUniversalAuthProvider Interface](https://msdn.microsoft.com/library/microsoft.sqlserver.dac.iuniversalauthprovider.aspx) (Interfaz IUniversalAuthProvider).
- La biblioteca administrada de ADAL que usa la autenticación universal de Azure AD con MFA se ha actualizado a la versión 3.13.9.
- Además, se ha publicado una nueva interfaz de CLI compatible con la configuración de administración de Azure AD para SQL Database y SQL Data Warehouse.

 Para obtener más información sobre los métodos de autenticación de Active Directory, vea [Autenticación universal con SQL Database y SQL Data Warehouse (compatibilidad de SSMS con MFA)](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication) y [Configurar Multi-Factor Authentication de Azure SQL Database para SQL Server Management Studio](https://docs.microsoft.com/azure/sql-database/sql-database-ssms-mfa-authentication-configure).

- La ventana de salida tiene entradas para las consultas que se ejecutan durante la expansión de los nodos del Explorador de objetos.



&nbsp;

&nbsp;

---

<a name="TitleNum_4"/>

### <a name="4-nbsp-create-and-update-database-tablesvisual-db-toolsdesign-tables-visual-database-toolsmd"></a>4. &nbsp; [Creación y actualización de tablas de bases de datos](visual-db-tools/design-tables-visual-database-tools.md)

*Actualización: 25-08-2017* &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; ([anterior](#TitleNum_3))

<!-- Source markdown line 30.  ms.author= "sstein".  -->

&nbsp;


<!-- git diff --ignore-all-space --unified=0 f63884ac2d04889e70c505cb5262c8dd81d73ee7 4b4c7aa5e8a0548405f02d11a66b722219fa78f0  (PR=2961  ,  Filename=design-tables-visual-database-tools.md  ,  Dirpath=docs\ssms\visual-db-tools\  ,  MergeCommitSha40=21f0cfd102a6fcc44dfc9151750f1b3c936aa053) -->



**Creación de una tabla**


1. Haga clic con el botón derecho en el nodo **Tablas** de la base de datos y seleccione **Crear** > **Tabla**:

    ![New table--../media/design-tables/new-table.png)

1. Agregue [columnas--column-properties-visual-database-tools.md) a la tabla:

    ![design table--../media/design-tables/new-table2.png)

1. Cierre el diseñador y guarde los cambios.

**Actualización de una tabla**


1. Haga clic con el botón derecho en la tabla situada en el nodo **Tablas** de la base de datos y seleccione **Diseñar**:

   ![Update table--../media/design-tables/update-table.png)

1. Actualice la configuración de la tabla según sea necesario:

   ![--../media/design-tables/update-table2.png)

1. Cierre el diseñador y guarde los cambios.

**Vea también**


[Tablas](http://msdn.microsoft.com/82d7819c-b801-4309-a849-baa63083e83f) [Propiedades de tabla (Visual Database Tools)--../../ssms/visual-db-tools/table-properties-visual-database-tools.md) [Propiedades de columna--column-properties-visual-database-tools.md) [Adición de columnas a una tabla--../../relational-databases/tables/add-columns-to-a-table-database-engine.md) [Claves principales y externas--../../relational-databases/tables/primary-and-foreign-key-constraints.md) [Índices--../../relational-databases/indexes/indexes.md) [Tipos de datos (Transact-SQL)--../../t-sql/data-types/data-types-transact-sql.md) [Descarga de SQL Server Management Studio (SSMS)--../download-sql-server-management-studio-ssms.md)







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



