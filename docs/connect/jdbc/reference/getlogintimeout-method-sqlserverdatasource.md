---
title: Método getLoginTimeout (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLoginTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 316f067c-9e08-456a-af19-b80b0bbd4a5c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5fe82d2709aa8efa32408a9d9d86f0f660bed823
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67982549"
---
# <a name="getlogintimeout-method-sqlserverdatasource"></a>Método getLoginTimeout (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de segundos que este objeto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) esperará mientras intenta realizar una conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getLoginTimeout()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un valor **int**que representa el número de segundos durante los que se esperará.  
  
## <a name="remarks"></a>Observaciones  
 Si la aplicación no especifica un valor de tiempo de forma explícita, este método devuelve un valor predeterminado de 15 segundos.  
  
 El método getLoginTimeout especifica este método getLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
