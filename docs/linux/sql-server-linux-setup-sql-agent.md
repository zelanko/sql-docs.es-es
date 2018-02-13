---
title: Instalar el Agente SQL Server en Linux | Documentos de Microsoft
description: "En este artículo se describe cómo instalar al Agente SQL Server en Linux."
author: rothja
ms.author: jroth
manager: craigg
ms.date: 10/02/2017
ms.topic: article
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: 
ms.suite: sql
ms.custom: sql-linux
ms.technology: database-engine
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.workload: On Demand
ms.openlocfilehash: 7db50a59a4a6ce9ab7aa416e4ac8d597449541b7
ms.sourcegitcommit: f02598eb8665a9c2dc01991c36f27943701fdd2d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/13/2018
---
# <a name="install-sql-server-agent-on-linux"></a>Instalar el Agente SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Los siguientes pasos instalación Agente SQL Server (**agente de server mssql**) en Linux. El [Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) ejecuta los trabajos programados de SQL Server. Para obtener información sobre las características compatibles con esta versión del Agente SQL Server, consulte el [notas de la versión](sql-server-linux-release-notes.md).

> [!NOTE]
> Antes de instalar el Agente SQL Server, en primer lugar [instalar SQL Server 2017](sql-server-linux-setup.md#platforms). Esto configura las claves y los repositorios de que se usa cuando instala el **agente de server mssql** paquete.

Instalar al Agente SQL Server para su plataforma:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

## <a name="RHEL">Instalar en RHEL</a>

Siga estos pasos para instalar el **agente de server mssql** en Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene **agente de server mssql** instalado, puede actualizar a la versión más reciente con los siguientes comandos:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Si tiene una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en el [notas de la versión](sql-server-linux-release-notes.md). A continuación, utilice los mismos pasos de instalación sin conexión se describe en el artículo [instalar SQL Server](sql-server-linux-setup.md#offline).

## <a name="ubuntu">Instalar en Ubuntu</a>

Siga estos pasos para instalar el **agente de server mssql** en Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene **agente de server mssql** instalado, puede actualizar a la versión más reciente con los siguientes comandos:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Si tiene una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en el [notas de la versión](sql-server-linux-release-notes.md). A continuación, utilice los mismos pasos de instalación sin conexión se describe en el artículo [instalar SQL Server](sql-server-linux-setup.md#offline).

## <a name="SLES">Instalar en SLES</a>

Siga estos pasos para instalar el **agente de server mssql** en SUSE Linux Enterprise Server. 

Instalar **mssql-server-agent** 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene **agente de server mssql** instalado, puede actualizar a la versión más reciente con los siguientes comandos:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Si tiene una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en el [notas de la versión](sql-server-linux-release-notes.md). A continuación, utilice los mismos pasos de instalación sin conexión se describe en el artículo [instalar SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo usar el Agente SQL Server para crear, programar y ejecutar trabajos, consulte [ejecutar un trabajo de agente SQL Server en Linux](sql-server-linux-run-sql-server-agent-job.md).
