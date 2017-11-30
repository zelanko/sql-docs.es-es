---
title: "' S New for SQL Server 2017 en Linux | Documentos de Microsoft"
description: Este tema destacan Novedades de SQL Server 2017 en Linux.
author: rothja
ms.author: jroth
manager: jhubbard
ms.date: 11/28/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: linux
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.workload: On Demand
ms.openlocfilehash: cdc32cffd67c794f5ec2d04ac7410892475f4f7f
ms.sourcegitcommit: d122a41cc953ba3e269c8709a18aa84f7c17982c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/29/2017
---
# <a name="whats-new-for-sql-server-2017-on-linux"></a>Novedades de SQL Server 2017 en Linux

[!INCLUDE[tsql-appliesto-sslinux-only](../includes/tsql-appliesto-sslinux-only.md)]

Este artículo describen las principales características y servicios disponibles para SQL Server 2017 ejecutando en Linux.

> [!NOTE]
> Además de estas capacidades en este artículo, las actualizaciones acumulativas se publican a intervalos regulares después de la versión de GA. Estas actualizaciones acumulativas proporcionan numerosas mejoras y correcciones. Para obtener información acerca de la versión CU más reciente, consulte [http://aka.ms/sql2017cu](http://aka.ms/sql2017cu). Para descargar los paquetes y los problemas conocidos, consulte el [notas de la versión](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server

- Habilita las capacidades básicas de motor de base de datos de SQL Server.
- Compatibilidad con las rutas de acceso de Linux nativo.
- Compatibilidad con IPv6.
- Compatibilidad con archivos de base de datos en NFS.
- Habilitado [transparente en seguridad de la capa](sql-server-linux-encrypted-connections.md) cifrado (TLS).
- Habilitado [autenticación de Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funcionalidad de grupos de disponibilidad](sql-server-linux-availability-group-overview.md) para lograr alta disponibilidad.
- [Búsqueda de texto completo](sql-server-linux-setup-full-text-search.md) admite.

## <a name="sql-server-agent"></a>Agente SQL Server

- Habilitado [Agente SQL Server](sql-server-linux-setup-sql-agent.md) admite para las siguientes tareas:
  - [Trabajos de Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Correo electrónico de base de datos](sql-server-linux-db-mail-sql-agent.md)
  - [Trasvase de registros](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Capacidad de ejecutar paquetes SSIS en Linux. Para obtener más información, consulte [configurar SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Otras mejoras

- Herramienta de configuración de línea de comandos, [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Compatibilidad con la instalación desatendida con [variables de entorno](sql-server-linux-configure-environment-variables.md).
- Multiplataforma [extensión de Visual Studio Code mssql server](sql-server-linux-develop-use-vscode.md).
- Generador de secuencias de comandos entre plataformas, [scripter mssql](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Monitor de vista de administración dinámica (DMV) multiplataforma, [herramienta DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Pasos siguientes

Para instalar a SQL Server en Linux, utilice uno de los siguientes tutoriales:

- [Instalar en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalar en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalar en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecutar en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=%2fsql%2flinux%2ftoc.json)

Por otra información con respecto a SQL Server en Linux, consulte la [Introducción](sql-server-linux-overview.md). Para descargar los paquetes y una lista de características no admitidas y los problemas conocidos, consulte el [notas de la versión](sql-server-linux-release-notes.md).

Para ver otras mejoras introducidas en SQL Server 2017, consulte [What's New en SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
