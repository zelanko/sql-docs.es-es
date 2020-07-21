---
title: dbmslpcn.dll ConnectionValidSharedMemory
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: b8fea72023f929fb01c8ee5ca699a1d695aa0788
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: es-ES
ms.lasthandoff: 07/06/2020
ms.locfileid: "86005741"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Función ConnectionValidSharedMemory en memoria compartida dbmslpcn.dll
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  La función determina si SQL Server memoria compartida está instalada y activa.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parámetros  
 *szServerName*  
  
-   Tipo: **Char \* **  
  
-   Nombre del servidor SQL Server.  
  
## <a name="return-value"></a>Valor devuelto  
 Tipo: **bool**  
  
 Devuelve 0 si no es válido; de lo contrario, devuelve un valor distinto de cero.  
  
  
