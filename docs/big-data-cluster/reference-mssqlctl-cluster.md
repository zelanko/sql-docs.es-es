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
ms.openlocfilehash: 088168e3400feea78fb9b92fa120f1140714ab34
ms.sourcegitcommit: 2533383a7baa03b62430018a006a339c0bd69af2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/01/2019
ms.locfileid: "57018431"
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
   [--accept-eula]
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