---
title: Notas de la versión de SQL Server 2019 | Microsoft Docs
ms.date: 02/28/2019
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 1afd1c7c1c3c142745e667662f51027218598e2f
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57017731"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas de la versión preliminar de SQL Server 2019
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen las limitaciones y los problemas conocidos de las versiones de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP). Para obtener información relacionada, consulte estos artículos:
- [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> Las versiones preliminares de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] están a su disposición para que pruebe las características de la próxima versión. No están admitidas para su uso en producción ni disponen de licencia para ello. Los siguientes escenarios no están admitidos de forma explícita:
>
> - Instalación en paralelo con otras versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> - Actualización de una instancia existente de SQL Server desde cualquier versión

**Pruebe [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]**
- [![Descargar desde el Centro de evaluación](../includes/media/download2.png)](https://go.microsoft.com/fwlink/?LinkID=862101) [Descargar [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para instalar en Windows](https://go.microsoft.com/fwlink/?LinkID=862101)
- Instalar en Linux para [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) y [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)
- [Ejecutar SQL Server 2019 en Docker](../linux/quickstart-install-connect-docker.md)

## <a name="ctp-23"></a>CTP 2.3
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3 es la versión pública más reciente de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3 está disponible únicamente como edición de evaluación. No hay más ediciones disponibles. La compatibilidad con CTP 2.3 se describe en `license_Eval.rtf` con el soporte de instalación.

Se puede detectar una compatibilidad limitada en una de las siguientes ubicaciones:

- Foros
  - [Comentarios de SQL Server](https://aka.ms/sqlfeedback)
  - [Introducción a SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [Documentación de SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- También puede enviar un tuit a [@SQLServer](https://twitter.com/SQLServer) con [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)

### <a name="documentation-ctp-23"></a>Documentación (CTP 2.3)

- **Problema e impacto en el cliente**: La documentación de SQL Server 2019 (15.x) es limitada, y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El contenido de los artículos específicos de SQL Server 2019 (15.x) se distinguirá con **Se aplica a**.

- **Problema e impacto en el cliente**: la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede filtrar por versión. Use el control situado en la parte superior izquierda de cada página de documentación para filtrar según sus requisitos. 

- **Problema e impacto en el cliente**: No hay ningún contenido sin conexión disponible para SQL Server 2019 (15.x).

### <a name="hardware-and-software-requirements-ctp-23"></a>Requisitos de hardware y software (CTP 2.3)

- **Problema e impacto en el cliente**: Los requisitos de hardware y software aún están en revisión y no son definitivos para la versión del producto.

  - **Hardware**
    - [Windows: requisitos de procesador, memoria y sistema operativo](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux: requisitos del sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 o una versión posterior. Para ver más requisitos, consulte [Requisitos para instalar SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - Microsoft .NET Framework 4.6.2. Disponible en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=53344).
    - En cuanto a Linux, consulte [Linux: Plataformas compatibles](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="updated-compiler"></a>Compilador actualizado

- **Problema e impacto en el cliente**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] incorpora un compilador actualizado. CTP 2.1 tenía un problema conocido por el que los resultados de un número de punto flotante y otros escenarios de conversión podían devolver un valor distinto al devuelto en versiones anteriores debido al compilador actualizado. CTP 2.2 incluye recursos para asegurarse de que los escenarios afectados devuelvan los mismos resultados que las versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. No se ha detectado ningún otro error en CTP 2.3. Notifique cualquier anomalía en los resultados en comparación con [!INCLUDE[ss2017](../includes/sssqlv14-md.md)] al equipo de [[!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] ](http://aka.ms/sqlfeedback) inmediatamente.

- **Solución**: N/D

- **Se aplica a**: SQL Server 2019 CTP 2.3, CTP 2.2 y CTP 2.1

### <a name="utf-8-collations"></a>Intercalaciones UTF-8

- **Problema e impacto en el cliente**: No se pueden usar las intercalaciones habilitadas para UTF-8 con algunas otras características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 no es compatible si se utilizan las siguientes características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

  - Servidor vinculado
  - OLTP en memoria
  - Tabla externa para PolyBase

  > [!Note]
  > Actualmente, no hay ninguna compatibilidad de interfaz de usuario para elegir intercalaciones habilitadas para UTF-8 en Azure Data Studio o SQL Server Data Tools (SSDT). La versión más reciente de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] (SSMS) permite elegir las intercalaciones habilitadas para UTF-8 en la interfaz de usuario.
 
- **Solución**: No hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3, CTP 2.2, CTP 2.1 y CTP 2.0.

### <a name="sql-graph"></a>SQL Graph

- **Problema e impacto en el cliente**: Las herramientas que dependen de la importación o exportación de tipo DacFx no funcionarán con las nuevas características de grafos: las restricciones perimetrales o la combinación de DML. La generación de scripts podría no funcionar en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

- **Solución**: La escritura de scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] y su ejecución en el servidor con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o SQLCMD sí funcionan. La exportación/importación de objetos de base de datos que crean restricciones perimetrales, que tienen la nueva sintaxis de combinación DML o que crean tablas/vistas derivadas en los objetos de grafos no funcionará. Los usuarios tendrán que crear manualmente estos objetos en su base de datos con scripts de [!INCLUDE[tsql](../includes/tsql-md.md)]. 

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3, CTP 2.2, CTP 2.1 y 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

- **Problema e impacto en el cliente**: Los cálculos completos tienen pendientes varias optimizaciones de rendimiento, incluida la funcionalidad limitada (sin indexación, etc.), y actualmente están deshabilitados de manera predeterminada.

- **Solución**: Para habilitar los cálculos completos, ejecute `DBCC traceon(127,-1)`. Para obtener más información, consulte [Habilitar cálculos completos](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3, 2.2, CTP 2.1 y 2.0.

### <a name="system-dynamic-management-views"></a>Vistas de administración dinámica del sistema +

- **Problema e impacto en el cliente**: La función con valores de tabla del sistema [sys.dm_db_objects_disabled_on_compatibility_level_change](../relational-databases/system-dynamic-management-views/spatial-data-sys-dm-db-objects-disabled-on-compatibility-level-change.md) devuelve valores aleatorios en la columna `dependency`.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3.

### <a name="sql-server-analysis-services-ssas"></a>SQL Server Analysis Services (SSAS)

- **Problema e impacto en el cliente**: para los modelos tabulares con seguridad dinámica, en algunas circunstancias un usuario puede ver datos de otro usuario que pertenece al mismo rol.

  **Escenario**: en el modelo hay al menos dos roles. Uno de los roles no tiene ninguna expresión de seguridad dinámica que contenga `USERNAME` o `USERPRINCIPALNAME`. El segundo rol con seguridad de nivel de fila dinámica se define para los usuarios A y B mediante expresiones que contienen `USERNAME` o `USERPRINCIPLENAME`. Los usuarios A y B se pueden conectar y consultar los datos, pero el usuario B puede ver datos protegidos solo para el usuario A en determinadas circunstancias.

- **Solución**: Agregue una medida ficticia al modelo. Por ejemplo, `[DummyMeasure] := UserName()`. Esto garantiza que se evalúan expresiones dinámicas para las expresiones de seguridad de nivel de fila.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.3.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
