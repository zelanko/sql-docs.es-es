---
title: SQL Server en Linux, preguntas más frecuentes | Microsoft Docs
description: En este artículo proporciona respuestas a las preguntas más frecuentes acerca de SQL Server que se ejecutan en Linux.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 07/17/2018
ms.topic: conceptual
ms.prod: sql
ms.component: ''
ms.suite: sql
ms.custom: sql-linux
ms.technology: linux
ms.openlocfilehash: 841c278d42fd3d2494bd1f08704797d5c11c235e
ms.sourcegitcommit: a431ca21eac82117492d7b84c398ddb3fced53cc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39102233"
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>SQL Server en Linux preguntas más frecuentes (P+F)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Las secciones siguientes proporcionan preguntas y respuestas frecuentes para SQL Server que se ejecutan en Linux.

## <a name="general-questions"></a>Preguntas generales

1. **¿Qué plataformas Linux son compatibles?**

   SQL Server se admite actualmente en Ubuntu, SUSE Linux Enterprise Server y Red Hat Enterprise Server. También admite que se ejecuta en un contenedor con Docker. Para obtener la información más reciente sobre las versiones admitidas, consulte [plataformas compatibles con](sql-server-linux-setup.md#supportedplatforms).

1. **¿SQL Server en Linux funciona en otras plataformas**?

   SQL Server se ha probado y compatible con Linux para las distribuciones enumeradas anteriormente. Otras distribuciones de Linux están estrechamente relacionadas y podría ser capaz de ejecutar SQL Server (por ejemplo, CentOS está estrechamente relacionada con Red Hat Enterprise Server). Pero si decide instalar SQL Server en un sistema operativo no compatible, revise el **directiva de soporte técnico** sección de la [directiva de soporte técnico para Microsoft SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server) para entender la compatibilidad implicaciones. Tenga en cuenta también que algunos community-mantienen las distribuciones de Linux no dispone de una manera formal para recibir soporte técnico si el sistema operativo subyacente es el problema.

1. **¿Qué características de SQL Server son compatibles con Linux?**

   Para obtener una lista completa de las características admitidas y problemas conocidos, consulte el [notas de la versión](sql-server-linux-release-notes.md).

1. **¿Qué es la directiva de soporte técnico para SQL Server?**

   Para entender la directiva de soporte técnico, revise el [política de asistencia técnica para SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Estoy procedentes de un fondo de Windows SQL Server. ¿Hay recursos para ayudar a obtener información sobre cómo usar SQL Server en Linux?**

   El [inicios rápidos](sql-server-linux-setup.md#platforms) proporcionan instrucciones paso a paso sobre cómo instalar SQL Server en Linux y ejecutar consultas Transact-SQL. Otros tutoriales proporcionan instrucciones adicionales sobre el uso de SQL Server en Linux. Para obtener una lista de otros fabricantes de sugerencias, consulte el [lista MSSQLTIPS de SQL Server en Linux sugerencias](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="installation"></a>Installation

1. **¿Cómo se puede obtener SQL Server instalada en Mis servidores Linux?**

   Microsoft mantiene repositorios de paquetes para instalar SQL Server y admite la instalación a través de los administradores de paquetes nativos como yum, zypper y piso. Para instalar rápidamente, consulte uno de los [inicios rápidos](sql-server-linux-setup.md#platforms).

1. **¿Puedo instalar a SQL Server en el subsistema de Linux para Windows 10?**

   No. Linux que se ejecutan en Windows 10 no es actualmente una plataforma compatible con SQL Server y las herramientas relacionadas.

1. **¿Qué sistemas de archivos de Linux puede usar SQL Server 2017 para archivos de datos?**

   Actualmente es compatible con SQL Server en Linux ext4 y XFS. Compatibilidad con otros sistemas de archivos se agregarán según sea necesario en el futuro.

1. **¿Puedo descargar los paquetes de instalación para instalar a SQL Server sin conexión?**

   Sí. Para obtener más información, vea el paquete de descarga de vínculos en el [notas de la versión](sql-server-linux-release-notes.md). Además, revise el [instrucciones para las instalaciones sin conexión](sql-server-linux-setup.md#offline).

1. **¿Puedo realizar una instalación desatendida de SQL Server en Linux?**

   Sí. Para obtener información de instalación desatendida, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md#unattended). Consulte los scripts de ejemplo para [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), y [Ubuntu](sample-unattended-install-ubuntu.md). También puede revisar [este script de ejemplo](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) creado por el equipo de asesoramiento de cliente de SQL Server.

## <a name="tools"></a>Herramientas

1. **¿Puedo usar al cliente de SQL Server Management Studio en Windows para tener acceso a SQL Server en Linux?**

   Sí, puede usar todas sus herramientas existentes que se ejecutan en Windows para tener acceso a SQL Server en Linux. Esto incluye las herramientas de Microsoft, como SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT) y sistemas operativos y herramientas de terceros.

1. **¿Hay una herramienta como SSMS que se ejecuta en Linux?**

   La nueva Microsoft SQL Operations Studio (preview) es una herramienta multiplataforma para la administración de SQL Server. Para obtener más información, consulte [¿qué es Microsoft SQL Operations Studio (versión preliminar)](../sql-operations-studio/what-is.md).

1. **¿Existen comandos como sqlcmd y bcp en Linux?**

   Sí, [sqlcmd y bcp](sql-server-linux-setup-tools.md) están disponibles de forma nativa en Linux, macOS y Windows. Además, usar el nuevo [mssql scripter](https://github.com/Microsoft/mssql-scripter) herramienta de línea de comandos en Windows, macOS o Linux para generar scripts de Transact-SQL para la base de datos SQL que ejecuta en cualquier. Consulte también la versión preliminar de la versión para [mssql-cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **¿Es posible ver al Monitor de actividad cuando se conecta a través de SSMS en Windows para una instancia ejecuta en Linux?**

   Sí, puede usar SSMS en Windows para conectarse de forma remota y use herramientas y características, como comandos de Monitor de actividad en una instancia de Linux.

1. **¿Qué herramientas están disponibles para supervisar el rendimiento de SQL Server en Linux?**

   Puede usar [vistas del sistema de administración dinámica (DMV)](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para recopilar distintos tipos de información acerca de SQL Server, incluida la información de proceso de Linux. Puede usar [Query Store](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) para mejorar el rendimiento de las consultas. Otras herramientas, como el integrado [panel rendimiento](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), funcionarán de forma remota en SQL Server Management Studio (SSMS) de Windows.

   > [!TIP]
   > Una manera de mejorar el rendimiento es configurar correctamente el sistema operativo Linux y el insance de SQL Server. Para obtener más información, consulte [procedimientos recomendados e instrucciones de configuración de SQL Server en Linux](sql-server-linux-performance-best-practices.md).

## <a name="administration"></a>Administración

1. **¿Microsoft ha creado una aplicación, como el Administrador de configuración de SQL Server en Linux?**

   Sí, hay una herramienta de configuración de SQL Server en Linux: [mssql-conf](sql-server-linux-configure-mssql-conf.md).

1. **¿SQL Server en Linux admite varias instancias en el mismo host?**

   Se recomienda ejecutar varios contenedores en un host para tener varias instancias distintas. Cada contenedor debe escuchar en un puerto diferente. Para obtener más información, consulte [ejecutar varios contenedores de SQL Server](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **¿Se admite la autenticación de Active Directory en Linux?**

   Sí. Para obtener más información, consulte [autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

1. **Son Always On y admite la agrupación en clústeres en Linux?**

   Agrupación en clústeres de conmutación por error y la alta disponibilidad en Linux se realizan con Pacemaker en Linux. Para obtener más información, consulte [continuidad empresarial y base de datos de recuperación: SQL Server en Linux](sql-server-linux-business-continuity-dr.md).

1. **¿Es posible configurar la replicación desde Linux a Windows y viceversa?**

   Las réplicas de escalado de lectura pueden utilizarse entre Windows y Linux para la replicación de datos unidireccional.

1. **¿Es posible migrar bases de datos existentes en versiones anteriores de SQL Server de Windows a Linux?**

   Sí, existen [varios métodos](sql-server-linux-migrate-overview.md) de conseguir esto.

1. **¿Puedo migrar Mis datos de Oracle y otros motores de base de datos a SQL Server en Linux?**

   Sí. SSMA admite la migración desde varios tipos de motores de base de datos: Microsoft Access, DB2, MySQL, Oracle y SAP ASE (anteriormente SAP Sybase ASE). Para obtener un ejemplo de cómo usar SSMA, consulte [migrar un esquema de Oracle a SQL Server 2017 en Linux con SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json).

1. **¿Qué permisos son necesarios para los archivos de SQL Server?**

   Todos los archivos de la `/var/opt/mssql` carpeta de archivos debe pertenecer a la **mssql** usuario y pertenecen a la **mssql** grupo. Tanto el **mssql** usuario y grupo deben tener permisos de lectura y escritura de todos los archivos y directorios. Tenga en cuenta los siguientes escenarios especiales que implican los permisos de archivos y directorios:

   * Permisos de propietario mssql y grupo son necesarios para los recursos compartidos de red montada que se usan para almacenar archivos de SQL Server.
   * Si encuentra los archivos de base de datos o copias de seguridad en un directorio que no sea predeterminado, también debe establecer permisos para ese directorio.
   * Si cambia la umask raíz predeterminada de 0022, se produce un error en la configuración de SQL Server después de la instalación. A continuación, debe aplicar manualmente los permisos necesarios para la cuenta de inicio de SQL Server.

1. **¿Puedo cambiar la propiedad de directorios y archivos de SQL Server desde la cuenta de mssql instalada y el grupo?**

   No se admite cambiar la propiedad de directorio de SQL Server y los archivos de la instalación predeterminada. La cuenta de mssql y grupo se utiliza específicamente para SQL Server y no tiene ningún acceso de inicio de sesión interactivo.

[!INCLUDE[Get Help Options](../includes/paragraph-content/get-help-options.md)]
