---
title: "Método registerOutParameter (int, int) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.registerOutParameter (int, int)
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 169229c7-b75d-498b-a5ac-df300424c909
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d25361cd32c4109e68550877cefbbcc7a8d8857b
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="registeroutparameter-method-int-int"></a>Método registerOutParameter (int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra el parámetro OUT en la posición ordinal especificada para el tipo JDBC determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un **int** que indica la posición ordinal del parámetro.  
  
 *sqlType*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método registerOutParameter especificado por el método registerOutParameter de la interfaz java.sql.CallableStatement.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, cuando *sqlType* es de tipo java.sql.Types.TIME, se modifica el comportamiento de este método mediante el **sendTimeAsDatetime** propiedad de conexión ([Estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Método registerOutParameter &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
