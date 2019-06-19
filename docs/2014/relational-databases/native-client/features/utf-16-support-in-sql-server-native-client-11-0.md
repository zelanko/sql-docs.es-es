---
title: Compatibilidad con UTF-16 en SQL Server Native Client 11.0 | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63205115"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Compatibilidad con UTF-16 en SQL Server Native Client 11.0
  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y si el `wchar` caracteres escritos en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un par suplente y si la siguiente `wchar` carácter es un punto de código suplente bajo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará el punto de código suplente alto en el búfer.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
