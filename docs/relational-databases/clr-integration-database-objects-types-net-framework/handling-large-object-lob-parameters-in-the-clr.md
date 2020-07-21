---
title: Administrar parámetros de objetos grandes (LOB) en CLR | Microsoft Docs
description: En este artículo se describe cómo administrar valores de objetos grandes (LOB) para parámetros en SQL Server la integración CLR. Use SqlBytes y SqlChars para los tipos LOB.
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
ms.openlocfilehash: 0b10ac8c1ac9ccba804b892617df0b8d6c0d2f14
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85637491"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Administrar parámetros de objetos grandes (LOB) en CLR
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use **SqlBytes** y **SqlChars** para pasar parámetros de tipo binario de objeto grande (LOB) (**varbinary (Max)**) y tipo de carácter LOB (**nvarchar (Max)**), respectivamente. Estos tipos permiten la transmisión por secuencias de los valores LOB de la base de datos a la rutina de Common Language Runtime (CLR), en lugar de copiar el valor completo en el espacio administrado. **SqlBinary** y **SqlString** solo se deben usar para los valores de cadena de caracteres y binarios pequeños.  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de datos de SQL Server en .NET Framework](../../relational-databases/clr-integration-database-objects-types-net-framework/sql-server-data-types-in-the-net-framework.md)  
  
  
