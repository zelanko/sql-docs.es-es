---
title: Compatibilidad con UTF-16
description: Obtenga información sobre la compatibilidad con UTF-16 en un búfer de longitud fija en SQL Server Native Client a partir de SQL Server 2012.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: f2520424-8ef4-409f-8147-d83da5076e96
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9b538c19ebb1c0841ffb4da5ec403f5986d626e2
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85719622"
---
# <a name="utf-16-support-in-sql-server-native-client-110"></a>Compatibilidad con UTF-16 en SQL Server Native Client 11.0
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asdw-pdw.md)]

  A partir de [!INCLUDE[ssSQL11](../../../includes/sssql11-md.md)], si proporciona un búfer de longitud fija al enlazar un parámetro de salida o el resultado de una columna y si el carácter **wchar** escrito en el búfer antes del carácter de terminación es un punto de código que actúa como suplente superior de un par de suplentes y el carácter **wchar** siguiente es un punto de código que actúa como suplente inferior, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no agregará el punto de código que actúa como suplente superior al búfer.  
  
## <a name="see-also"></a>Consulte también  
 [Características de SQL Server Native Client](../../../relational-databases/native-client/features/sql-server-native-client-features.md)  
  
  
