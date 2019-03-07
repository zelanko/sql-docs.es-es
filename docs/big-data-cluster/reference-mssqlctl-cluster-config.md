---
title: referencia de configuración de clúster mssqlctl
titleSuffix: SQL Server 2019 big data clusters
description: Artículo de referencia para los comandos de clúster mssqlctl.
author: rothja
ms.author: jroth
manager: craigg
ms.date: 02/28/2019
ms.topic: reference
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 26e93151a1150bbbbd1798b38486ca5b01aaab1d
ms.sourcegitcommit: d7ed341b2c635dcdd6b0f5f4751bb919a75a6dfe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/06/2019
ms.locfileid: "57527208"
---
# <a name="mssqlctl-cluster-config"></a>configuración del clúster mssqlctl

El siguiente artículo proporciona la referencia para la **cluster config** comandos en el **mssqlctl** herramienta. Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md).

## <a id="commands"></a> Comandos

|||
|---|---|
| [get](#get) | Obtenga el clúster. |

## <a id="get"></a> obtener la configuración del clúster mssqlctl

Obtenga el clúster.

```
mssqlctl cluster config get
   --name
   --output-file
```

### <a name="parameters"></a>Parámetros

| Parámetros | Descripción |
|---|---|
| **--name -n** | Nombre del clúster, usado para el espacio de nombres de kubernetes. Requerido. |
| **--output-file -f** | Archivo de salida para almacenar el resultado en. Requerido. |

## <a name="next-steps"></a>Pasos siguientes

Para obtener más información acerca de otros **mssqlctl** comandos, consulte [mssqlctl referencia](reference-mssqlctl.md). Para obtener más información sobre cómo instalar el **mssqlctl** herramienta, consulte [instalar mssqlctl para administrar clústeres de SQL Server 2019 macrodatos](deploy-install-mssqlctl.md).