---
title: Manejo de parámetros de objetos grandes (LOB) en el CLR ? Microsoft Docs
description: En este artículo se describe cómo controlar los valores de objetos grandes (LOB) para los parámetros de la integración de CLR de SQL ServerSQL Server . Use SqlBytes y SqlChars para tipos LOB.
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
author: rothja
ms.author: jroth
ms.openlocfilehash: 0941ca2f5fc1a05397dd3dbec5e0dd27c6e5d815
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488468"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Administrar parámetros de objetos grandes (LOB) en CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Utilice **SqlBytes** y **SqlChars** para pasar parámetros de tipo binario de objeto grande (LOB) (**varbinary(max)**) y tipo de carácter LOB (**nvarchar(max)**), respectivamente. Estos tipos permiten la transmisión por secuencias de los valores LOB de la base de datos a la rutina de Common Language Runtime (CLR), en lugar de copiar el valor completo en el espacio administrado. **SqlBinary** y **SqlString** solo se deben usar para valores de cadena binarios y de caracteres pequeños.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
