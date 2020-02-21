---
title: Método isCurrency (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isCurrency
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7fe25d90-693c-4d3b-9dd2-0f8351c5a9ed
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 33d21e8bfe8a774d8b5b21584ba9fd3f02246f4e
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67977684"
---
# <a name="iscurrency-method-sqlserverresultsetmetadata"></a>Método isCurrency (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si la columna designada es un valor de efectivo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isCurrency(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si la columna es un valor de efectivo. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método isCurrency especifica este método isCurrency en la interfaz java.sql.ResultSetMetaData.  
  
 Este método solamente devolverá **true** con tipos de datos money y smallmoney de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
