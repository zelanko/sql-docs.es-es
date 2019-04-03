---
title: referencia de clúster mssqlctl
titleSuffix: SQL Server big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e4e54ac3c7206ad8a6592c8cfe0b45d9ea4b8fd8
ms.sourcegitcommit: 2de5446fbc57787f18a907dd5deb02a7831ec07d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/02/2019
ms.locfileid: "58860476"
---
# <a name="mssqlctl-cluster"></a>Clúster mssqlctl

[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

El siguiente artículo proporciona la referencia para la **clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [crear](#create) | Crear el clúster. |
| [eliminar](#delete) | Eliminar el clúster. |
| [config](reference-mssqlctl-cluster-config.md) | Comandos de configuración del clúster. |
| [debug](reference-mssqlctl-cluster-debug.md) | Comandos de depuración. |

## <a id="create"></a> crear clúster mssqlctl

Crear el clúster.

```
mssqlctl cluster create
   --name
   --accept-eula
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre del clúster, usado para el espacio de nombres de kubernetes. |
| **--accept-eula -e** | ¿Acepta los términos de licencia? \[Sí/no\].  Los valores permitidos: no, sí. Requerido. |

## <a id="delete"></a> mssqlctl cluster delete

Eliminar el clúster.

```
mssqlctl cluster delete
   --name
   [--force]
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **: nombre - n** | Nombre del clúster, usado para el espacio de nombres de kubernetes. Requerido. |
| **--forzar -f** | Clúster de eliminación de fuerza. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).