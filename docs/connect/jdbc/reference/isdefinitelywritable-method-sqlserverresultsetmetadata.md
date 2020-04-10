---
title: Método isDefinitelyWritable (SQLServerResultSetMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSetMetaData.isDefinitelyWritable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 7650e89a-dc8e-43ca-8eb2-f962f1a4b4ae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28b64f5cbc9de40057a9015c19eef96c21f93260
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80923601"
---
# <a name="isdefinitelywritable-method-sqlserverresultsetmetadata"></a>Método isDefinitelyWritable (SQLServerResultSetMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Indica si se realizará correctamente la operación de escritura en una columna designada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean isDefinitelyWritable(int column)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *column*  
  
 Valor **int** que indica el índice de la columna.  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si la escritura de la columna se realizará correctamente. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método isDefinitelyWritable especifica este método isDefinitelyWritable en la interfaz java.sql.ResultSetMetaData.  
  
> [!NOTE]  
>  Cuando se usa el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devolverá siempre false.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-methods.md)   
 [Miembros SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-members.md)   
 [Clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md)  
  
  
