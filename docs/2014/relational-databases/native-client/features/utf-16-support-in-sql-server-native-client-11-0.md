---
title: Compatibilidad con UTF-16 en SQL Server Native Client 11,0 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 415cb2fe8a3295770cfc8bd2d5c6e56750adb6d9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63205115"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Compatibilidad con UTF-16 en SQL Server Native Client 11.0
  A partir [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)]de, si se proporciona un búfer de longitud fija al enlazar un resultado de columna o un parámetro `wchar` de salida y si el carácter escrito en el búfer antes del carácter de terminación es un punto de código suplente alto de un `wchar` par suplente, y si el siguiente carácter [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] es un punto de código suplente bajo, Native Client no agregará el punto de código suplente alto al búfer.  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
