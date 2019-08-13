---
title: Novedades de SQL Server 2017 en Linux
description: En este artículo se destacan las novedades de SQL Server 2017 en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 04/23/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 456b6f31-6b97-4e31-80ab-b40151ec4868
ms.openlocfilehash: 3f3f51716acf69368ae2554446c47d125b500e03
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032161"
---
# <a name="whats-new-for-sql-server-on-linux"></a>Novedades de SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

En este artículo se describen las características y los servicios principales disponibles para SQL Server 2017 en ejecución en Linux.

Se ha publicado la versión preliminar de SQL Server 2019. En este artículo no se trata la versión preliminar de SQL Server 2019. Para obtener información sobre la versión preliminar de SQL Server 2019, vea [Novedades de la versión preliminar de SQL Server 2019 para Linux](../sql-server/what-s-new-in-sql-server-ver15.md?view=sql-server-ver15#sql-server-on-linux).

> [!NOTE]
> Además de las funcionalidades de este artículo, se publican actualizaciones acumulativas a intervalos regulares después del lanzamiento de GA. Estas actualizaciones acumulativas proporcionan muchas mejoras y correcciones. Para obtener información sobre la versión de CU más reciente, consulte [https://aka.ms/sql2017cu](https://aka.ms/sql2017cu). Para descargar los paquetes y consultar los problemas conocidos, vea [Notas de la versión](sql-server-linux-release-notes.md).

## <a name="sql-server-database-engine"></a>Motor de base de datos de SQL Server

- Se han habilitado las funcionalidades principales del motor de base de datos de SQL Server.
- Compatibilidad con rutas de acceso nativas de Linux.
- Compatibilidad con IPv6.
- Compatibilidad con archivos de base de datos en NFS.
- Se ha habilitado el cifrado de [Seguridad de la capa de transporte](sql-server-linux-encrypted-connections.md) (TLS).
- Se ha habilitado la [autenticación de Azure Active Directory](sql-server-linux-active-directory-authentication.md).
- [Funcionalidad de grupos de disponibilidad](sql-server-linux-availability-group-overview.md) para la alta disponibilidad.
- Compatibilidad con la [búsqueda de texto completo](sql-server-linux-setup-full-text-search.md).

## <a name="sql-server-agent"></a>Agente SQL Server

- Se ha habilitado la compatibilidad del [Agente SQL Server](sql-server-linux-setup-sql-agent.md) con las siguientes tareas:
  - [Trabajos de Transact-SQL](sql-server-linux-run-sql-server-agent-job.md)
  - [Correo electrónico de base de datos](sql-server-linux-db-mail-sql-agent.md)
  - [Trasvase de registros](sql-server-linux-use-log-shipping.md)

## <a name="sql-server-integration-services-ssis"></a>SQL Server Integration Services (SSIS)

- Capacidad de ejecutar paquetes SSIS en Linux. Para obtener más información, vea [Configuración de SQL Server Integration Services en Linux con ssis-conf](sql-server-linux-configure-ssis.md).

## <a name="other-improvements"></a>Otras mejoras

- Herramienta de configuración de la línea de comandos, [mssql-conf](sql-server-linux-configure-mssql-conf.md).
- Compatibilidad de la instalación desatendida con las [variables de entorno](sql-server-linux-configure-environment-variables.md).
- [Extensión de mssql-server de Visual Studio Code](sql-server-linux-develop-use-vscode.md) multiplataforma.
- Generador de scripts multiplataforma, [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli/blob/dev/doc/usage_guide.md).
- Supervisión de la vista de administración dinámica (DMV) multiplataforma, [herramienta DBFS](https://github.com/Microsoft/dbfs).

## <a name="next-steps"></a>Pasos siguientes

Para instalar SQL Server en Linux, use uno de los siguientes tutoriales:

- [Instalación en Red Hat Enterprise Linux](quickstart-install-connect-red-hat.md)
- [Instalación en SUSE Linux Enterprise Server](quickstart-install-connect-suse.md)
- [Instalación en Ubuntu](quickstart-install-connect-ubuntu.md)
- [Ejecución en Docker](quickstart-install-connect-docker.md)
- [Aprovisionar una máquina virtual de SQL en Azure](/azure/virtual-machines/linux/sql/provision-sql-server-linux-virtual-machine?toc=/sql/toc/toc.json)

Para ver otras mejoras presentadas en SQL Server 2017, consulte [Novedades de SQL Server 2017](../sql-server/what-s-new-in-sql-server-2017.md).

> [!TIP]
> Para obtener respuesta a las preguntas más frecuentes, vea [Preguntas más frecuentes sobre SQL Server en Linux](sql-server-linux-faq.md).

[!INCLUDE[get-help-options](../includes/paragraph-content/get-help-options.md)]
