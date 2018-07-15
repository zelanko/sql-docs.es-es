---
title: Administrar parámetros de objetos grandes (LOB) en el CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- large data, CLR integration
- LOB data [SQL Server], CLR integration
- SqlBytes data type
- SqlChars data type
ms.assetid: d07956f6-9543-4476-9426-536f95991150
caps.latest.revision: 20
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: f23f42a01ba5268c9165a79f5330fb0efcc538ce
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353237"
---
# <a name="handling-large-object-lob-parameters-in-the-clr"></a>Administrar parámetros de objetos grandes (LOB) en CLR
  Use `SqlBytes` y `SqlChars` para pasar parámetros de tipo binario de objeto grande (LOB) (`varbinary(max)`) y de tipo de caracteres LOB (`nvarchar(max)`), respectivamente. Estos tipos permiten la transmisión por secuencias de los valores LOB de la base de datos a la rutina de Common Language Runtime (CLR), en lugar de copiar el valor completo en el espacio administrado. `SqlBinary` y `SqlString` solo se deben usar para los valores de cadenas de caracteres y binarios pequeños.  
  
## <a name="see-also"></a>Vea también  
 [Tipos de datos de SQL Server en .NET Framework](sql-server-data-types-in-the-net-framework.md)  
  
  
