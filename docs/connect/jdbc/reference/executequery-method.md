---
title: Método executeQuery () | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerPreparedStatement.executeQuery ()
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 1d90407f-16df-4ba2-b4a5-47d5751e1d7c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: efe1c815b7ed4cee971399e6b71d9d21254e10c1
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922002"
---
# <a name="executequery-method-"></a>Método executeQuery ()
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ejecuta la consulta SQL en este objeto [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) y devuelve el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) que genera la consulta.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet executeQuery()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto SQLServerResultSet.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método executeQuery especifica este método executeQuery en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método executeQuery &#40;SQLServerPreparedStatement&#41;](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
