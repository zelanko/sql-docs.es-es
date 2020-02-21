---
title: Método getDate (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: aa9f08af-df24-4c80-8298-c4007339b20a
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2d959dc2f9372aa723089dc87bea66424c4d2ea8
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67984021"
---
# <a name="getdate-method-int"></a>Método getDate (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Date en el lenguaje de programación Java según el índice de parámetro especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Date getDate(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un valor **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Date.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getDate especifica este método getDate en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve una fecha válida que forma parte de un tipo de datos **datetime** o **smalldatetime** de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], con la parte correspondiente a la hora establecida en la hora de inicio de Java de 00:00 (media noche).  
  
## <a name="see-also"></a>Consulte también  
 [Método getDate &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
