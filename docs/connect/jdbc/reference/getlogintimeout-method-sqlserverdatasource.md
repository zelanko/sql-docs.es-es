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
manager: craigg
ms.openlocfilehash: 26a7c8e0cc876c8d13e9beb621354cead2f6296c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47708583"
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
  
## <a name="remarks"></a>Notas  
 Si la aplicación no especifica un valor de tiempo de forma explícita, este método devuelve un valor predeterminado de 15 segundos.  
  
 Este método getLoginTimeout especificado por el método getLoginTimeout en la interfaz javax.sql.DataSource.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
