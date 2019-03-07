---
title: referencia de clúster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 130d3019d49deb7851696f6a1db2f77040734b31
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527218"
---
# <a name="mssqlctl-cluster"></a>clúster mssqlctl

El siguiente artículo proporciona la referencia para la **clúster** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [create](#create) | Crear el clúster. |
| [delete](#delete) | Eliminar el clúster. |
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
| **--name -n** | Nombre del clúster, usado para el espacio de nombres de kubernetes. |
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
| **--name -n** | Nombre del clúster, usado para el espacio de nombres de kubernetes. Requerido. |
| **--force -f** | Clúster de eliminación de fuerza. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).