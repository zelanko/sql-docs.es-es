---
title: Compatibilidad con UTF-16 en SQL Server Native Client 11.0 | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b97b4cdb57ec40c99cb9856362d7fdc65e705e5f
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39554715"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Compatibilidad con UTF-16 en SQL Server Native Client 11.0
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si proporciona un búfer de longitud fija al enlazar un parámetro de salida o el resultado de una columna y si el carácter **wchar** escrito en el búfer antes del carácter de terminación es un punto de código que actúa como suplente superior de un par de suplentes y el carácter **wchar** siguiente es un punto de código que actúa como suplente inferior, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará el punto de código que actúa como suplente superior al búfer.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
