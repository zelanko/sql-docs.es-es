---
title: Referencia de mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: b050638ee0ca600c5df0ecdbe5616b801f41e7a8
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/18/2019
ms.locfileid: "58860357"
---
# <a name="mssqlctl"></a>mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **mssqlctl** herramienta para [clústeres de macrodatos de 2019 de SQL Server (versión preliminar)](big-data-cluster-overview.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [app](reference-mssqlctl-app.md) | Crear, eliminar, ejecutar y administrar aplicaciones. |
| [cluster](reference-mssqlctl-cluster.md) | Seleccione, administrar y operar los clústeres. |
| [login](#login) | Inicie sesión en el clúster. |
| [logout](#logout) | Cerrar la sesión de clúster. |
| [storage](reference-mssqlctl-storage.md) | Administrar el almacenamiento de clúster. |

## <a id="login"></a> inicio de sesión mssqlctl

Inicie sesión en el clúster.

```
mssqlctl login
   --endpoint
   --password
   --username
```

### <a name="parameters"></a>Parámetros

| Parámetro | Descripción |
|---|---|
|**--endpoint -e**| Clúster de host y puerto (ex) `http://host:port"`. |
|**--password -p**| Credenciales de contraseña. |
|**--username -u**| Usuario de la cuenta. |

### <a name="examples"></a>Ejemplos

Sesión de forma interactiva.

```
mssqlctl login
```

Inicie sesión con el nombre de usuario y contraseña.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret
```

Inicie sesión con el nombre de usuario, contraseña y el punto de conexión de clúster.

```
mssqlctl login -u johndoe@contoso.com -p VerySecret --endpoint https://host.com:12800
```

## <a id="logout"></a> mssqlctl logout

Cerrar la sesión de clúster.

```
mssqlctl logout
   --username
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--username -u** | Usuario de la cuenta, si faltan, cierre de sesión la cuenta activa actual. |

### <a name="examples"></a>Ejemplos

Cierra la sesión este usuario.

```
mssqlctl logout --username admin
```

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).