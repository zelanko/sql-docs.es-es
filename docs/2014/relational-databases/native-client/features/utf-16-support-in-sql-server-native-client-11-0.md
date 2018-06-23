---
title: Compatibilidad con UTF-16 en SQL Server Native Client 11.0 | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 66198f42676944967a2d655f14a27470922fd318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36200346"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Compatibilidad con UTF-16 en SQL Server Native Client 11.0
  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si se proporciona un búfer de longitud fija al enlazar un parámetro de resultado o salida de la columna y si el `wchar` carácter escrito en el búfer antes de que el carácter de terminación es un punto de código suplente alto de un par suplente y si la siguiente `wchar` carácter es un punto de código suplente bajo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará el punto de código suplente alto en el búfer.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  