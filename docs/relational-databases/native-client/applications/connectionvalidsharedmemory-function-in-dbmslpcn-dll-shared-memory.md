---
title: ConnectionValidSharedMemory dbmslpcn. dll
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 6ae35826-7d75-4542-b686-5f79316b6157
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9c64fe0020ca6c406cadd5b5b71ade1641919a81
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "75244200"
---
# <a name="connectionvalidsharedmemory-function-in-dbmslpcndll-shared-memory"></a>Función ConnectionValidSharedMemory en memoria compartida dbmslpcn.dll
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  La función determina si SQL Server memoria compartida está instalada y activa.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
BOOL ConnectionValidSharedMemory(char * szServerName);  
```  
  
## <a name="parameters"></a>Parámetros  
 *szServerName*  
  
-   Tipo: **Char\* **  
  
-   Nombre del servidor SQL Server.  
  
## <a name="return-value"></a>Valor devuelto  
 Tipo: **bool**  
  
 Devuelve 0 si no es válido; de lo contrario, devuelve un valor distinto de cero.  
  
  
