---
title: Notas de la versión de SQL Server 2019 | Microsoft Docs
ms.custom: ''
ms.date: 09/25/2018
ms.prod: sql-server-2018
ms.reviewer: ''
ms.technology:
- server-general
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: e7c4447ce03c25eab91e62c03540906d29714d7f
ms.sourcegitcommit: 13d98701ecd681f0bce9ca5c6456e593dfd1c471
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 10/18/2018
ms.locfileid: "49419107"
---
# <a name="sql-server-2019-preview-release-notes"></a>Notas de la versión preliminar de SQL Server 2019

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

En este artículo se describen las limitaciones y los problemas conocidos de las versiones de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] Community Technology Preview (CTP). Para obtener información relacionada, consulte estos artículos:
- [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md)

> [!NOTE]
> Las versiones preliminares de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] están a su disposición para que pruebe las características de la próxima versión. No están admitidas para su uso en producción ni disponen de licencia para ello. Los siguientes escenarios no están admitidos de forma explícita:
>
> - Instalación en paralelo con otras versiones de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]
> - Desinstalación
> - Actualización desde una edición anterior de SQL Server

**Pruebe [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)]**
- [![Descargar desde el Centro de evaluación](../includes/media/download2.png)](http://go.microsoft.com/fwlink/?LinkID=862101) [Descargar [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] para instalar en Windows](http://go.microsoft.com/fwlink/?LinkID=862101)
- Instalar en Linux para [Red Hat Enterprise Server](../linux/quickstart-install-connect-red-hat.md), [SUSE Linux Enterprise Server](../linux/quickstart-install-connect-suse.md) y [Ubuntu](../linux/quickstart-install-connect-ubuntu.md)
- [Ejecutar SQL Server 2019 en Docker](../linux/quickstart-install-connect-docker.md)

## <a name="ctp-20-september-2018"></a>CTP 2.0 (septiembre de 2018)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 es la primera versión pública de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 está disponible únicamente como edición de evaluación. No hay más ediciones disponibles. La compatibilidad con CTP 2.0 se describe en license_Eval.rtf con su soporte de instalación.

Se puede detectar una compatibilidad limitada en una de las siguientes ubicaciones:

- Foros
  - [Comentarios de SQL Server](http://aka.ms/sqlfeedback)
  - [Introducción a SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [Documentación de SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- También puede enviar un tuit a [@SQLServer](http://twitter.com/SQLServer) con [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)

### <a name="documentation-ctp-20"></a>Documentación (CTP 2.0)

- **Problema e impacto en el cliente:** la documentación de SQL Server 2019 (15.x) es limitada y el contenido está incluido en el conjunto de documentación de [!INCLUDE[ssSQL17](../includes/sssql17-md.md)]. El contenido de los artículos específicos de SQL Server 2019 (15.x) se distinguirá con **Se aplica a**.

- **Problema e impacto en el cliente**: la documentación de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se puede filtrar por versión. Use el control situado en la parte superior izquierda de cada página de documentación para filtrar según sus requisitos. 

- **Problema e impacto en el cliente:** no hay ningún contenido sin conexión disponible para SQL Server 2019 (15.x).

### <a name="hardware-and-software-requirements"></a>Requisitos de hardware y de software

- **Problema e impacto en el cliente**: los requisitos de hardware y de software aún están en revisión y no son definitivos para la versión del producto.

  - **Hardware**
    - [Windows: requisitos de procesador, memoria y sistema operativo](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md#pmosr)
    - [Linux: requisitos del sistema](../linux/sql-server-linux-setup.md#system)
  - **Software**
    - Windows Server 2016 o una versión posterior. Para ver más requisitos, consulte [Requisitos para instalar SQL Server](../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)
    - En cuanto a Linux, consulte [Linux: Plataformas compatibles](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="sql-graph"></a>SQL Graph

**Problema e impacto en el cliente**: las herramientas que tienen dependencias en la importación/exportación de tipo DacFx no funcionarán con las nuevas características de gráficos: las restricciones perimetrales o la combinación de DML. La generación de scripts podría no funcionar en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

**Solución alternativa**: la escritura de scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] y su ejecución en el servidor con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o SQLCMD sí funcionan. La exportación/importación de objetos de base de datos que crean restricciones perimetrales, que tienen la nueva sintaxis de combinación DML o que crean tablas/vistas derivadas en los objetos de gráficos no funcionará. Los usuarios tendrán que crear manualmente estos objetos en su base de datos con scripts de [!INCLUDE[tsql](../includes/tsql-md.md)]. 

**Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

### <a name="utf-8-collations"></a>Intercalaciones UTF-8

**Problema e impacto en el cliente**: no se pueden usar las intercalaciones habilitadas para UTF-8 con algunas otras características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 no es compatible si se utilizan las siguientes características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

- Replicación de SQL Server
- Servidor vinculado
- OLTP en memoria
- Tabla externa para PolyBase

  Observe también que actualmente no hay ninguna compatibilidad de interfaz de usuario para elegir intercalaciones habilitadas para UTF-8 en Azure Data Studio o SSDT. La versión más reciente de SSMS permite elegir las intercalaciones habilitadas para UTF-8 en la interfaz de usuario.

**Solución alternativa**: no hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

**Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

### <a name="lightweight-query-profiling-infrastructure"></a>Infraestructura de generación de perfiles ligera de consultas

**Problema e impacto en el cliente**: la ejecución del comando `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` devuelve un error de sintaxis. Se producirá un error en todos los escenarios que dependan de la ejecución de este comando.

> [!NOTE]
> Actualmente, la infraestructura de generación de perfiles ligera de consultas (LWP) no se puede controlar al nivel de base de datos individual y permanece habilitada para todas las bases de datos de forma predeterminada. Para obtener más información sobre LWP, consulte [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

**Solución alternativa**: no hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

**Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

**Problema e impacto en el cliente**: los cálculos completos tienen pendientes varias optimizaciones de rendimiento, incluida la funcionalidad limitada (sin indexación, etc.), y actualmente están deshabilitados de manera predeterminada.

**Solución alternativa**: para habilitar los cálculos completos, ejecute `DBCC traceon(127,-1)`. Para obtener más información, consulte [Habilitar cálculos completos](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

**Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>Tarea de transferencia de base de datos de SQL Server Integration Services (SSIS)

**Problema e impacto en el cliente**: si se configura una `Transfer Database Task` para transferir una base de datos en el modo `Database Online`, se puede producir el siguiente error:

>El método Execute de la tarea ha devuelto el código de error 0x80131500 (An error occurred while transferring data. See the inner exception for details.) [Se ha producido un error al transferir los datos. Vea la excepción interna para obtener detalles.]. El método Execute debe ejecutarse correctamente e indicar el resultado con un parámetro "out".

**Solución alternativa**: ejecute `DBCC TRACEON (7416,-1)` en el servidor y vuelva a intentarlo.

### <a name="sql-server-machine-learning-services-installation-failure"></a>Error de instalación de SQL Server Machine Learning Services

**Problema e impacto en el cliente**: se produce un error en las instalaciones de SQL Server Machine Learning Services en los equipos que tienen problemas de relación de confianza con el dominio principal. En este caso, en los registros aparecerá el siguiente error:
 
>  Error: 0 : System.SystemException:The trust relationship between this workstation and the primary domain failed at System.Security.Principal.NTAccount.TranslateToSids(IdentityReferenceCollection sourceAccounts, Boolean& someFailed) ...

Compruébelo en los registros ubicados en:

* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\R_SERVICES\library\RevoScaleR\rxLibs\x64\RegisterRExt.log`
* `C:\Program Files\Microsoft SQL Server\MSSQL15.MSSQLSERVER\PYTHON_SERVICES\Lib\site-packages\revoscalepy\rxLibs\RegisterRExt.log`
**Solución alternativa**: resuelva los problemas de confianza del dominio y repita la instalación.

**Se aplica a**: SQL Server 2019 CTP 2.0.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
