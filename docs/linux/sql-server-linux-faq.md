---
title: "SQL Server en Linux preguntas más frecuentes | Documentos de Microsoft"
description: "Este artículo proporciona respuestas a preguntas frecuentes acerca de SQL Server que se ejecute en Linux."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 12/21/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: sql-linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.workload: Active
ms.openlocfilehash: 2da90e6cdf49531980e9014075d7b094b61271fd
ms.sourcegitcommit: b4fd145c27bc60a94e9ee6cf749ce75420562e6b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2018
---
# <a name="sql-server-on-linux-frequently-asked-questions-faq"></a>SQL Server en Linux preguntas más frecuentes (P+F)

Las secciones siguientes proporcionan preguntas y respuestas más comunes para SQL Server ejecutando en Linux.

## <a name="general-questions"></a>Preguntas generales

1. **¿En qué plataformas Linux son compatibles?**

   SQL Server se admite actualmente en Red Hat Enterprise Server, SUSE Linux Enterprise Server y Ubuntu. Para ver la información más reciente acerca de las versiones compatibles, consulte [las plataformas admitidas](sql-server-linux-setup.md#supportedplatforms).

1. **¿Las características de SQL Server admitidas en Linux?**

   Para obtener una lista completa de las características admitidas y los problemas conocidos, consulte el [notas de la versión](sql-server-linux-release-notes.md).

1. **¿Qué es la directiva de soporte técnico para SQL Server?**

   Para comprender la directiva de soporte técnico, revise la [política de asistencia técnica para SQL Server](https://support.microsoft.com/help/4047326/support-policy-for-microsoft-sql-server).

1. **Estoy procedentes de un fondo de Windows SQL Server. ¿Hay recursos para ayudarle a aprender a usar SQL Server en Linux?**

   El [tutoriales](sql-server-linux-setup.md#platforms) se proporcionan instrucciones paso a paso sobre cómo instalar SQL Server en Linux y ejecutar consultas Transact-SQL. Otros tutoriales proporcionan instrucciones adicionales sobre el uso de SQL Server en Linux. Para una lista de aplicaciones de terceros de sugerencias, vea la [lista MSSQLTIPS de SQL Server en Linux sugerencias](https://www.mssqltips.com/sql-server-tip-category/226/sql-server-on-linux/).

## <a name="installation"></a>Installation

1. **¿Cómo se puede obtener SQL Server instalada en Mis servidores Linux?**

   Microsoft mantiene repositorios de paquete para la instalación de SQL Server y admite la instalación a través de los administradores de paquetes nativo como yum, zypper y piso. Para instalar rápidamente, vea uno de los [tutoriales](sql-server-linux-setup.md#platforms).

1. **¿Puedo instalar a SQL Server en el subsistema de Linux para Windows 10?**

   No. Linux que se ejecuta en Windows 10 no es actualmente una plataforma compatible con SQL Server y las herramientas relacionadas.

1. **¿Los sistemas de archivos de Linux pueden usar SQL Server 2017 para archivos de datos?**

   Actualmente SQL Server en Linux es compatible con ext4 y XFS. Compatibilidad con otros sistemas de archivos se agregarán según sea necesario en el futuro.

1. **¿Se puede descargar los paquetes de instalación para instalar a SQL Server sin conexión?**

   Sí. Para obtener más información, vea el paquete de descarga de vínculos en la [notas de la versión](sql-server-linux-release-notes.md). Además, revise la [instrucciones para instalaciones sin conexión](sql-server-linux-setup.md#offline).

1. **¿Puedo realizar una instalación desatendida de SQL Server en Linux?**

   Sí. Para obtener información de instalación desatendida, consulte [Guía de instalación para SQL Server en Linux](sql-server-linux-setup.md#unattended). Vea las secuencias de comandos de ejemplo para [Red Hat](sample-unattended-install-redhat.md), [SUSE Linux Enterprise Server](sample-unattended-install-suse.md), y [Ubuntu](sample-unattended-install-ubuntu.md). También puede revisar [este script de ejemplo](https://blogs.msdn.microsoft.com/sqlcat/2017/10/03/unattended-install-and-configuration-for-sql-server-2017-on-linux/) creado por el equipo de asesoramiento de cliente de SQL Server.

## <a name="tools"></a>Herramientas

1. **¿Puedo usar al cliente de SQL Server Management Studio en Windows para tener acceso a SQL Server en Linux?**

   Sí, puede usar todas sus herramientas existentes que se ejecutan en Windows para tener acceso a SQL Server en Linux. Esto incluye herramientas de Microsoft, como SQL Server Management Studio (SSMS), SQL Server Data Tools (SSDT) y sistemas operativos y herramientas de otros fabricantes.

1. **¿Hay una herramienta como SSMS que se ejecuta en Linux?**

   La nueva Microsoft SQL operaciones Studio (vista previa) es una herramienta multiplataforma para la administración de SQL Server. Para obtener más información, consulte [¿qué es Microsoft SQL operaciones Studio (versión preliminar)](../sql-operations-studio/what-is.md).

1. **¿Encontrará los comandos, como sqlcmd y bcp en Linux?**

   Sí, [sqlcmd y bcp](sql-server-linux-setup-tools.md) están disponibles de forma nativa en Linux, Mac OS y Windows. Además, use la nueva [scripter mssql](https://github.com/Microsoft/mssql-scripter) herramienta de línea de comandos en Linux, Mac OS o Windows para generar scripts de T-SQL para su base de datos SQL que se ejecuta desde cualquier lugar. Además, vea la vista previa de la versión para [mssql cli](https://blogs.technet.microsoft.com/dataplatforminsider/2017/12/12/try-mssql-cli-a-new-interactive-command-line-tool-for-sql-server/).

1. **¿Es posible ver al Monitor de actividad cuando se conecta a través de SSMS en Windows para una instancia ejecutan en Linux?**

   Sí, puede usar SSMS en Windows para conectarse de forma remota y use herramientas y características que los comandos de Monitor de actividad en una instancia de Linux.

1. **¿Qué herramientas están disponibles para supervisar el rendimiento de SQL Server en Linux?**

   Puede usar [vistas de administración dinámica (DMV) de sistema](../relational-databases/system-dynamic-management-views/system-dynamic-management-views.md) para recopilar distintos tipos de información acerca de SQL Server, incluida la información de proceso de Linux. Puede usar [almacén de consultas](../relational-databases/performance/monitoring-performance-by-using-the-query-store.md) para mejorar el rendimiento de las consultas. Otras herramientas, como la integrada [panel de rendimiento](https://blogs.msdn.microsoft.com/sql_server_team/new-in-ssms-performance-dashboard-built-in/), funcionan de forma remota en SQL Server Management Studio (SSMS) de Windows.

## <a name="administration"></a>Administración

1. **¿Microsoft ha creado una aplicación como el Administrador de configuración de SQL Server en Linux?**

   Sí, hay una herramienta de configuración de SQL Server en Linux: [mssql-conf](sql-server-linux-configure-mssql-conf.md).

1. **¿SQL Server en Linux admite varias instancias en el mismo host?**

   Se recomienda ejecutar varios contenedores en un host para tener varias instancias distintos. Cada contenedor debe escuchar en un puerto diferente. Para obtener más información, consulte [ejecutar varios contenedores de SQL Server](sql-server-linux-configure-docker.md#run-multiple-sql-server-containers).

1. **¿Se admite la autenticación de Active Directory en Linux?**

   Sí. Para obtener más información, consulte [autenticación de Active Directory con SQL Server en Linux](sql-server-linux-active-directory-authentication.md).

1. **Son Always On y agrupación en clústeres admite en Linux?**

   Agrupación en clústeres de conmutación por error y la alta disponibilidad en Linux se realizan con marcapasos en Linux. Para obtener más información, consulte [continuidad empresarial y base de datos de recuperación: SQL Server en Linux](sql-server-linux-business-continuity-dr.md).

1. **¿Es posible configurar la replicación de Linux en Windows y viceversa?**

   Réplicas de escala de lectura se pueden utilizar entre Windows y Linux para la replicación de datos unidireccional.

1. **¿Es posible migrar las bases de datos existentes en versiones anteriores de SQL Server de Windows para Linux?**

   Sí, hay [varios métodos](sql-server-linux-migrate-overview.md) de conseguirlo.

1. **¿Puedo migrar Mis datos de Oracle y otros motores de base de datos a SQL Server en Linux?**

   Sí. SSMA admite la migración desde varios tipos de motores de base de datos: Microsoft Access, DB2, MySQL, Oracle y SAP ASE (anteriormente SAP Sybase ASE). Para obtener un ejemplo de cómo usar SSMA, consulte [migrar un esquema de Oracle a SQL Server 2017 en Linux con SQL Server Migration Assistant](../ssma/oracle/sql-server-linux-convert-from-oracle.md?toc=%2fsql%2flinux%2ftoc.json).

1. **¿Qué permisos son necesarios para los archivos de SQL Server?**

   Todos los archivos de la `/var/opt/mssql` debe ser propiedad de carpeta de archivos de la **mssql** usuario y pertenecen a la **mssql** grupo. Tanto el **mssql** usuario y grupo deben tener permisos de lectura y escritura de todos los archivos y directorios. Tenga en cuenta los siguientes escenarios especiales relacionadas con los permisos de archivos y directorios:

   * Para mssql propietario y el grupo se requieren permisos para recursos compartidos de red montada que se utilizan para almacenar archivos de SQL Server.
   * Si encuentra los archivos de base de datos o las copias de seguridad en un directorio no predeterminado, también debe establecer permisos para ese directorio.
   * Si cambia el umask raíz predeterminada de 0022, se produce un error en la configuración de SQL Server después de la instalación. A continuación, debe aplicar manualmente permisos necesarios para la cuenta de inicio de SQL Server.

1. **¿Puedo cambiar la propiedad de directorios y archivos de SQL Server de la cuenta de mssql instalada y el grupo?**

   No se admite cambiar la propiedad de directorio de SQL Server y los archivos de la instalación predeterminada. La cuenta de mssql y el grupo se utiliza específicamente para SQL Server y no tiene acceso de inicio de sesión interactivo.

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de cómo ejecutar SQL Server en Linux, consulte la [información general de SQL Server en Linux](sql-server-linux-overview.md).