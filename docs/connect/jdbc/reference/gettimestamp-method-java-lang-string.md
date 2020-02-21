---
title: Método getTimestamp (java.lang.String) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4d5174db-365c-4476-9472-7871578ef34c
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 999cfba0f0bd98bfc7e13f436303160ef66962b3
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978732"
---
# <a name="gettimestamp-method-javalangstring"></a>Método getTimestamp (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Timestamp en el lenguaje de programación Java según el nombre de parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String sCol)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Timestamp.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTimestamp especifica este método getTimestamp en la interfaz java.sql.CallableStatement.  
  
 Este método solamente devuelve valores de columnas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** y **smalldatetime**.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTimestamp &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
