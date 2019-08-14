---
title: Instalación de PolyBase en Linux
titlesuffix: SQL Server
description: En este artículo, se describe cómo instalar SQL Server PolyBase en Linux.
author: aboke
ms.author: aboke
ms.date: 4/12/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: linux
ms.openlocfilehash: 3c53eb5db9238f1da32cb207dafb9e36b7748914
ms.sourcegitcommit: 63c6f3758aaacb8b72462c2002282d3582460e0b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/25/2019
ms.locfileid: "68495355"
---
# <a name="install-polybase-on-linux"></a>Instalación de PolyBase en Linux

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-linuxonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-linuxonly.md)]

Siga estos pasos para instalar [PolyBase](../../relational-databases/search/full-text-search.md) (**mssql-server-polybase**) en Linux. PolyBase le permite ejecutar consultas externas en orígenes de datos remotos. 

>[!NOTE]
> Antes de la instalación de Polybase, se tiene que [instalar SQL Server](../../linux/sql-server-linux-setup.md#platforms). Esto configura las claves y los repositorios que se usan para instalar el paquete **mssql-server-polybase**.

> Actualmente la escalabilidad horizontal de PolyBase en Linux está deshabilitada.


Instalación de PolyBase en el sistema operativo:

- [Red Hat Enterprise Linux](#RHEL)
- [Ubuntu](#ubuntu)
- [SUSE Linux Enterprise Server](#SLES)



## <a name="RHEL">Instalación en RHEL</a>

Use el comando siguiente para instalar el paquete **mssql-server-polybase** en Red Hat Enterprise Linux. 

```bash
sudo yum install -y mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Después de la instalación, debe [habilitar la característica PolyBase](#enable).

Si necesita una instalación sin conexión, busque la descarga del paquete PolyBase en [Notas de la versión](../../linux/sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name="ubuntu">Instalación en Ubuntu</a>

Use el comando siguiente para instalar el paquete **mssql-server-polybase** en Ubuntu. 

```bash
sudo apt-get install mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Después de la instalación, debe [habilitar la característica PolyBase](#enable).

Si necesita una instalación sin conexión, busque la descarga del paquete PolyBase en [Notas de la versión](../../linux/sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](../../linux/sql-server-linux-setup.md#offline).

## <a name="SLES">Instalación en SLES</a>

Use los comandos siguientes para instalar el paquete **mssql-server-polybase** en SUSE Linux Enterprise Server. 

```bash
sudo zypper install mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```bash
sudo systemctl restart mssql-server
```

>[!NOTE]
>Después de la instalación, debe [habilitar la característica PolyBase](#enable).


Si necesita una instalación sin conexión, busque la descarga del paquete PolyBase en [Notas de la versión](../../linux/sql-server-linux-release-notes.md). Luego use los mismos pasos de instalación sin conexión descritos en el artículo [Instalar SQL Server](../../linux/sql-server-linux-setup.md#offline).


## <a name="enable">Habilitación de PolyBase</a> 

Tras la instalación, se debe habilitar PolyBase para acceder a sus características. Conéctese a la instancia de SQL Server instalada y use el comando de Transact-SQL siguiente para habilitarlo.

```sql
exec sp_configure @configname = 'polybase enabled', @configvalue = 1;
RECONFIGURE [WITH OVERRIDE];
```

## <a name="update-polybase"></a>Actualización de PolyBase

Si ya tiene **mssql-server-polybase** instalado, se puede actualizar a la versión más reciente con los comandos siguientes:

### <a name="rhel"></a>RHEL

```bash
sudo yum remove -y mssql-server-polybase
sudo yum check-update
sudo yum install -y mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```
sudo systemctl restart mssql-server
```

### <a name="ubuntu"></a>Ubuntu

```bash
sudo apt-get remove mssql-server-polybase
sudo apt-get update 
sudo apt-get install mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```
sudo systemctl restart mssql-server
```

### <a name="sles"></a>SLES

```bash
sudo zypper remove mssql-server-polybase
sudo zypper refresh
sudo zypper install mssql-server-polybase
```

Se le pedirá que reinicie la instancia de SQL Server. Para ello, use el comando siguiente.

```
sudo systemctl restart mssql-server
```

>[!NOTE]
>Después de la instalación, debe [habilitar la característica PolyBase](#enable).

## <a name="next-steps"></a>Pasos siguientes

PolyBase en Linux puede tener acceso a los orígenes de datos siguientes. Siga los vínculos proporcionados para obtener más información sobre cómo crear una tabla externa a partir de estos orígenes cuando PolyBase está habilitado. 

- [SQL Server (además de SQL DB y Azure SQL Data Warehouse)](../../relational-databases/polybase/polybase-configure-sql-server.md)
- [Oracle](../../relational-databases/polybase/polybase-configure-oracle.md)
- [Teradata](../../relational-databases/polybase/polybase-configure-teradata.md)
- [MongoDB (y Cosmos DB)](../../relational-databases/polybase/polybase-configure-mongodb.md)

Para obtener más información sobre cómo se usa, consulte el artículo de referencia de Transact-SQL relativo a [CREATE EXTERNAL TABLE](../../t-sql/statements/create-external-table-transact-sql.md).
