---
title: referencia de mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artículo de referencia para los comandos mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: be1ece46bd171370a91273c832bf89a0bf426cd3
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018371"
---
# <a name="mssqlctl"></a>mssqlctl

El siguiente artículo proporciona la referencia para la **mssqlctl** herramienta para los clústeres de macrodatos de 2019 de SQL Server (versión preliminar).

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