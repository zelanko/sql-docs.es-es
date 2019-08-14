---
title: Instalación del Agente SQL Server en Linux
description: En este artículo se explica cómo instalar el Agente SQL Server en Linux.
author: VanMSFT
ms.author: vanto
ms.date: 02/20/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.assetid: 77f16adc-e6cb-4a57-82f3-7b9780369868
ms.openlocfilehash: c27a31a5e6b9ed771df82e942087d7be88270038
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68032470"
---
# <a name="install-sql-server-agent-on-linux"></a>Instalación del Agente SQL Server en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

 El [Agente SQL Server](https://docs.microsoft.com/sql/ssms/agent/sql-server-agent) ejecuta trabajos programados de SQL Server. A partir de SQL Server 2017 CU4, el Agente SQL Server se incluye con el paquete **mssql-server** y está deshabilitado de forma predeterminada. Para obtener información sobre las características admitidas en esta versión del Agente SQL Server junto con información de versión, vea las [Notas de la versión](sql-server-linux-release-notes.md).

 Instale o habilite el Agente SQL Server:
- [En las versiones 2017 CU4 y posteriores, habilite el Agente SQL Server](#EnableAgentAfterCU4)
- [En las versiones 2017 CU3 y anteriores, instale el Agente SQL Server](#InstallAgentBelowCU4)


## <a name="EnableAgentAfterCU4">En las versiones 2017 CU4 y posteriores, habilite el Agente SQL Server</a>

 Para habilitar el Agente SQL Server, siga los pasos siguientes.

```bash
sudo /opt/mssql/bin/mssql-conf set sqlagent.enabled true 
sudo systemctl restart mssql-server
```

> [!NOTE]
> Si va a actualizar desde 2017 CU3 o anterior con el agente instalado, el Agente SQL Server se habilita automáticamente y se desinstalan los paquetes anteriores.  

## <a name="InstallAgentBelowCU4">En las versiones 2017 CU3 y anteriores, instale el Agente SQL Server</a>

> [!NOTE]
> Las instrucciones de instalación siguientes se aplican a SQL Server versiones 2017 CU3 y anteriores. Antes de instalar el Agente SQL Server, [instale SQL Server](sql-server-linux-setup.md#platforms). Con esto se configuran las claves y los repositorios que se usan al instalar el paquete **mssql-server-agent**.

Instale el Agente SQL Server para la plataforma:
- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)

### <a name="RHEL">Instalación en RHEL</a>

Use los pasos siguientes para instalar **mssql-server-agent** en Red Hat Enterprise Linux. 

```bash
sudo yum install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene instalado **mssql-server-agent**, puede actualizar a la versión más reciente con los comandos siguientes:

```bash
sudo yum check-update
sudo yum update mssql-server-agent
sudo systemctl restart mssql-server
```

Si necesita una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en las [Notas de la versión](sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](sql-server-linux-setup.md#offline).

### <a name="ubuntu">Instalación en Ubuntu</a>

Use los siguientes pasos para instalar **mssql-server-agent** en Ubuntu. 

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene instalado **mssql-server-agent**, puede actualizar a la versión más reciente con los comandos siguientes:

```bash
sudo apt-get update 
sudo apt-get install mssql-server-agent
sudo systemctl restart mssql-server
```

Si necesita una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en las [Notas de la versión](sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](sql-server-linux-setup.md#offline).

### <a name="SLES">Instalación en SLES</a>

Use los pasos siguientes para instalar **mssql-server-agent** en SUSE Linux Enterprise Server. 

Instale **mssql-server-agent**. 

```bash
sudo zypper install mssql-server-agent
sudo systemctl restart mssql-server
```

Si ya tiene instalado **mssql-server-agent**, puede actualizar a la versión más reciente con los comandos siguientes:

```bash
sudo zypper refresh
sudo zypper update mssql-server-agent
sudo systemctl restart mssql-server
```

Si necesita una instalación sin conexión, busque la descarga del paquete del Agente SQL Server en las [Notas de la versión](sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](sql-server-linux-setup.md#offline).

## <a name="next-steps"></a>Pasos siguientes
Para obtener más información sobre cómo usar el Agente SQL Server para crear, programar y ejecutar trabajos, vea [Ejecución de un trabajo del Agente SQL Server en Linux](sql-server-linux-run-sql-server-agent-job.md).
