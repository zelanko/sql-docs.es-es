---
description: Método getByte (int) (SQLServerResultSet)
title: Método getByte (int) (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getByte (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b22ba097-6cb8-4c5d-916b-6360dd01d2c5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8a94b4ca24a0d00ca45837e230cc3465e8728ffc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88437087"
---
# <a name="getbyte-method-int-sqlserverresultset"></a>Método getByte (int) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del índice de columna designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un valor **byte** en el lenguaje de programación Java.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public byte getByte(int columnIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *columnIndex*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor de **byte**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getByte especifica este método getByte en la interfaz java.sql.ResultSet.  
  
 Este método solo se admite en los tipos de datos [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que pueden devolver de forma segura un valor de bytes, como por ejemplo, tinyint y bit. El resto de tipos de datos producirá una excepción.  
  
## <a name="see-also"></a>Consulte también  
 [Método getByte &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
