---
title: Método setSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 705a0494-b5e2-43db-940a-1b8cec550cdb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 293667d8e3e06fb5eda7a74fdeed58c89fb0f1ae
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67972959"
---
# <a name="setsendtimeasdatetime-method-sqlserverdatasource"></a>Método setSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Modifica el valor de la propiedad de conexión **sendTimeAsDatetime**.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setSendTimeAsDatetime(boolean sendTimeAsDateTime)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sendTimeAsDateTime*  
  
 Valor booleano. Cuando sea TRUE, produce valores java.sql.Time que se envían al servidor como tipos **datetime** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Cuando sea FALSE, produce valores java.sql.Time que se envían al servidor como tipos **time** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Observaciones  
 [SQLServerDataSource.getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md) devuelve el valor de la propiedad de conexión **sendTimeAsDatetime**.  
  
 Para más información sobre la propiedad de conexión **sendTimeAsDatetime**, consulte [Establecimiento de las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md).  
  
 Para más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
