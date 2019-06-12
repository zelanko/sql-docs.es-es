---
title: Interfaz ISQLServerPreparedStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: cf87892e-5c34-4ac6-8258-c2a81e117b26
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6defd8b451089c70969f7b8efca5fec41d6af258
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66796434"
---
# <a name="isqlserverpreparedstatement-interface"></a>Interfaz ISQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa la implementación básica de la funcionalidad de la instrucción preparada de JDBC. Esta interfaz se agregó en el controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.sql.PreparedStatement, [ISQLServerStatement](../../../connect/jdbc/reference/isqlserverstatement-interface.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public interface ISQLServerPreparedStatement  
```  
  
## <a name="remarks"></a>Notas  
 Esta interfaz se implementa mediante [clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
 Esta interfaz expone los siguientes métodos específicos del [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]:  
  
|Método|Para obtener más información, vea|  
|------------|-------------------------------|  
|public void setDateTimeOffset(int, microsoft.sql.DateTimeOffset)|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
