---
title: Notas de la versión de SQL Server 2019 | Microsoft Docs
ms.date: 11/06/2018
ms.prod: sql
ms.reviewer: ''
ms.technology: release-landing
ms.topic: article
ms.assetid: 13942af8-5a40-4cef-80f5-918386767a47
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: = sql-server-ver15 || = sqlallproducts-allversions
ms.openlocfilehash: 2c21ac917845b8162348b93fec3b868f1f748592
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51703863"
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

## <a name="ctp-21-november-2018"></a>CTP 2.1 (noviembre de 2018)
[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 es la versión pública más reciente de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 está disponible únicamente como edición de evaluación. No hay más ediciones disponibles. La compatibilidad con CTP 2.1 se describe en license_Eval.rtf con su soporte de instalación.

Se puede detectar una compatibilidad limitada en una de las siguientes ubicaciones:

- Foros
  - [Comentarios de SQL Server](https://aka.ms/sqlfeedback)
  - [Introducción a SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqlgetstarted)
  - [Transact-SQL](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=transactsql)
  - [Documentación de SQL Server](https://social.msdn.microsoft.com/Forums/sqlserver/en-US/home?forum=sqldocumentation)

- También puede enviar un tuit a [@SQLServer](https://twitter.com/SQLServer) con [#sqlhelp](https://twitter.com/search?q=%23sqlhelp)

### <a name="documentation-ctp-21"></a>Documentación (CTP 2.1)

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
    - Microsoft .NET Framework 4.6.2. Disponible en el [Centro de descarga](https://www.microsoft.com/download/details.aspx?id=53344).
    - En cuanto a Linux, consulte [Linux: Plataformas compatibles](../linux/sql-server-linux-setup.md#supportedplatforms)

### <a name="floating-point-results"></a>Resultados del número de punto flotante

- **Problema e impacto en el usuario**: la versión preliminar de SQL Server 2019 usa un compilador actualizado para compilar SQL Server. En algunos casos, el código compilado con el nuevo compilador puede devolver valores numéricos de punto flotante que son diferentes de las versiones anteriores de SQL Server. El cambio de comportamiento se dará solo en el nuevo nivel de compatibilidad (150) en una futura versión de CTP.

- **Solución**: N/D

- **Se aplica a**: SQL Server 2019 CTP 2.1

### <a name="sql-server-integration-services-ssis-page-deployment-after-switching-db-to-single-user-mode-and-then-switching-back"></a>Implementación de la página de SQL Server Integration Services (SSIS) después de cambiar la base de datos al modo de usuario único y luego volver a cambiar

- **Problema e impacto en el usuario**: una vez que SSISB se cambie del modo de usuario único al modo de varios usuarios, es posible que aparezca el siguiente error al implementar un paquete:

  `Cannot continue the execution because the session is in the kill state.`

- **Solución**: detenga y reinicie la instancia de SQL Server y cambie de nuevo SSISDB al modo de varios usuarios. 

- **Se aplica a:** versión preliminar de SQL Server 2019 CTP 2.1


### <a name="udf-inlining"></a>Inserción de UDF 

- **Problema e impacto en el usuario**: hay escenarios de casos extremos en que las llamadas anidadas a inserciones de funciones definidas por el usuario no validan correctamente la seguridad.
  
- **Solución**: deshabilite la inserción de UDF para estas UDF con el parámetro `INLINE = OFF`.

- **Se aplica a**: SQL Server 2019 CTP 2.1

### <a name="lightweight-query-profiling-infrastructure"></a>Infraestructura de generación de perfiles ligera de consultas

- **Problema e impacto en el cliente**: la ejecución del comando `ALTER DATABASE SCOPED CONFIGURATION SET LIGHTWEIGHT_QUERY_PROFILING = ON` devuelve un error de sintaxis. Se producirá un error en todos los escenarios que dependan de la ejecución de este comando.

  > [!NOTE]
  > Actualmente, la infraestructura de generación de perfiles ligera de consultas (LWP) no se puede controlar al nivel de base de datos individual y permanece habilitada para todas las bases de datos de forma predeterminada. Para más información sobre LWP, vea [Novedades de SQL Server 2019](../sql-server/what-s-new-in-sql-server-ver15.md).

- **Solución**: no hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1 y CTP 2.0.

### <a name="utf-8-collations"></a>Intercalaciones UTF-8

- **Problema e impacto en el cliente**: no se pueden usar las intercalaciones habilitadas para UTF-8 con algunas otras características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. UTF-8 no es compatible si se utilizan las siguientes características de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:

  - Replicación de SQL Server
  - Servidor vinculado
  - OLTP en memoria
  - Tabla externa para PolyBase

    Observe también que actualmente no hay ninguna compatibilidad de interfaz de usuario para elegir intercalaciones habilitadas para UTF-8 en Azure Data Studio o SSDT. La versión más reciente de SSMS permite elegir las intercalaciones habilitadas para UTF-8 en la interfaz de usuario.

- **Solución**: no hay ninguna solución alternativa para [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1, CTP 2.0.

### <a name="sql-graph"></a>SQL Graph

- **Problema e impacto en el usuario**: las herramientas que dependen de la importación/exportación de tipo DacFx no funcionarán con las nuevas características de grafos: las restricciones perimetrales o la combinación de DML. La generación de scripts podría no funcionar en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].

- **Solución alternativa**: la escritura de scripts de [!INCLUDE[tsql](../includes/tsql-md.md)] y su ejecución en el servidor con [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] o SQLCMD sí funcionan. La exportación/importación de objetos de base de datos que crean restricciones perimetrales, que tienen la nueva sintaxis de combinación DML o que crean tablas/vistas derivadas en los objetos de grafos no funcionará. Los usuarios tendrán que crear manualmente estos objetos en su base de datos con scripts de [!INCLUDE[tsql](../includes/tsql-md.md)]. 

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1, 2.0.

### <a name="always-encrypted-with-secure-enclaves"></a>Always Encrypted con enclaves seguros

- **Problema e impacto en el usuario**: los cálculos completos tienen pendientes varias optimizaciones de rendimiento, incluida la funcionalidad limitada (sin indexación, etc.), y actualmente están deshabilitados de manera predeterminada.

- **Solución alternativa**: para habilitar los cálculos completos, ejecute `DBCC traceon(127,-1)`. Para obtener más información, consulte [Habilitar cálculos completos](../relational-databases/security/encryption/configure-always-encrypted-enclaves.md#configure-a-secure-enclave).

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.1, 2.0.

### <a name="sql-server-integration-service---fuzzy-lookup-transformation"></a>Servicio de integración de SQL Server: transformación de búsqueda aproximada

- **Problema e impacto en el usuario**: la transformación de búsqueda aproximada produciría el siguiente error si se configura para reutilizar el índice:

  `The specified delimiters do not match the delimiters used to build the pre-existing match index "...". This error occurs when the delimiters used to tokenize fields do not match. This can have unknown effects on the matching behavior or results.`

- **Solución**: N/D

- **Más información**: N/D  

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP2.1

## <a name="ctp-20-september-2018"></a>CTP 2.0 (septiembre de 2018)

[!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0 es la primera versión pública de [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)].

### <a name="sql-server-integration-services-ssis-transfer-database-task"></a>Tarea de transferencia de base de datos de SQL Server Integration Services (SSIS)

- **Problema e impacto en el cliente**: si se configura una `Transfer Database Task` para transferir una base de datos en el modo `Database Online`, se puede producir el siguiente error:

  >El método Execute de la tarea ha devuelto el código de error 0x80131500 (An error occurred while transferring data. See the inner exception for details.) [Se ha producido un error al transferir los datos. Vea la excepción interna para obtener detalles.]. El método Execute debe ejecutarse correctamente e indicar el resultado con un parámetro "out".

- **Solución alternativa**: ejecute `DBCC TRACEON (7416,-1)` en el servidor y vuelva a intentarlo.

- **Se aplica a**: [!INCLUDE[SQL Server 2019](../includes/sssqlv15-md.md)] CTP 2.0.

[!INCLUDE[get-help-options-msft-only](../includes/paragraph-content/get-help-options.md)]

![MS_Logo_X-Small](../sql-server/media/ms-logo-x-small.png)
