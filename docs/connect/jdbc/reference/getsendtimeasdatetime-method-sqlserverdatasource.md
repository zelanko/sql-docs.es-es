---
title: "Método getSendTimeAsDatetime (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
caps.latest.revision: "15"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: f784b25fe9390d98d32ab31e6f3f837e30aa746b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>Método getSendTimeAsDatetime (SQLServerDataSource) 
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0.  
  
 Devuelve el valor de la **sendTimeAsDatetime** propiedad de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si los valores de java.sql.Time se enviarán al servidor como un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** tipo. **false** si los valores de java.sql.Time se enviarán al servidor como un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **tiempo** tipo.  
  
## <a name="remarks"></a>Comentarios  
 Vea [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md) para obtener más información sobre la **sendTimeAsDatetime** propiedad de conexión.  
  
 [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) permite establecer mediante programación el **sendTimeAsDatetime** propiedad de conexión.  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
