---
title: Método getColumnDisplaySize (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.getColumnDisplaySize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 21c25443-bd2b-4b60-9798-4efe2c158952
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 60ed53f51ff9fe828944ecfdbadab647501eac5c
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923414"
---
# <a name="getcolumndisplaysize-method-sqlserverresultsetmetadata"></a>Método getColumnDisplaySize (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el ancho máximo normal, en caracteres, de la columna designada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getColumnDisplaySize(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **int** que indica el ancho máximo. Si se desconoce el ancho, devuelve 0.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getColumnDisplaySize especifica este método getColumnDisplaySize en la interfaz java.sql.ResultSetMetaData.  
  
 El controlador JDBC 3.0 de [!INCLUDE[msCoName](../../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] incorpora cambios de comportamiento en la columna COLUMN_SIZE. Vea [SQLServerDatabaseMetaData.getColumns](../../../connect/jdbc/reference/getcolumns-method-sqlserverdatabasemetadata.md) para más información.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
