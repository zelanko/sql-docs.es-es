---
title: Método getSendTimeAsDatetime (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 02287122-5dc1-455d-987f-95fd9a69d503
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 36cdeda1cdad226c00449d118f154fd555e7246d
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66792090"
---
# <a name="getsendtimeasdatetime-method-sqlserverdatasource"></a>Método getSendTimeAsDatetime (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Este método se agregó en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] JDBC Driver 3.0.  
  
 Devuelve el valor de la **sendTimeAsDatetime** propiedad de conexión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getSendTimeAsDatetime();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si los valores java.sql.Time se enviarán al servidor como un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** tipo. **false** si los valores java.sql.Time se enviarán al servidor como un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **tiempo** tipo.  
  
## <a name="remarks"></a>Notas  
 Consulte [estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md) para obtener más información sobre la **sendTimeAsDatetime** propiedad de conexión.  
  
 Con [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md) puede establecer mediante programación la propiedad de conexión **sendTimeAsDatetime**.  
  
 Para más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
