---
title: allow polybase export (opción de configuración del servidor) | Microsoft Docs
description: Establecimiento de la opción de configuración `allow polybase export` en SQL Server
ms.custom: ''
ms.date: 07/10/2020
ms.prod: sql
ms.prod_service: ''
ms.reviewer: ''
ms.technology: polybase
ms.topic: conceptual
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: c25a7e42b55561ed6337281497e847999d722292
ms.sourcegitcommit: dacd9b6f90e6772a778a3235fb69412662572d02
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2020
ms.locfileid: "86279658"
---
# <a name="set-allow-polybase-export-configuration-option"></a>Establecimiento de la opción de configuración `allow polybase export`

[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

La opción de configuración del servidor `allow polybase export` permite `INSERT` en una tabla externa de Hadoop. 

Esta característica no admite la inserción en otros orígenes de datos externos.

 En la siguiente tabla se describen los valores posibles: 

| Value | Significado                                |
|-------|----------------------------------------|
| 0     | Deshabilitado. Esta es la configuración predeterminada. |
| 1     | habilitado                                |


Esta configuración surte efecto inmediatamente.

## <a name="example"></a>Ejemplo

En el ejemplo siguiente se habilita este valor.

```sql
sp_configure 'show advanced options', 1;
GO
RECONFIGURE;
GO
sp_configure 'allow polybase export', 0;
GO
RECONFIGURE;
GO
```

## <a name="next-steps"></a>Pasos siguientes

 [Exportar datos](../../relational-databases/polybase/polybase-configure-hadoop.md#exporting-data)