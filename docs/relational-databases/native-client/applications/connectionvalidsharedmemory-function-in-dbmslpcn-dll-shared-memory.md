---
title: "Función ConnectionValidSharedMemory en dbmslpcn.dll Shared Memory | Documentos de Microsoft"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client|applications
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: de8df92448f4a873b5e1489a4c66c2e36db651dc
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Función ConnectionValidSharedMemory en dbmslpcn.dll memoria compartida
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  La función determina si la memoria compartida de SQL Server está instalado y activo.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parámetros  
 *szServerName*  
  
-   Tipo: **char\***  
  
-   El nombre de SQL server.  
  
## <a name="return-value"></a>Valor devuelto  
 Tipo: **BOOL**  
  
 Devuelve 0 si no es válido; en caso contrario, devuelve es distinto de cero.  
  
  
