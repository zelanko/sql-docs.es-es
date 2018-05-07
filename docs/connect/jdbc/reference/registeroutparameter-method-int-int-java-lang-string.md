---
title: Método registerOutParameter (int, int, java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, java.lang.String)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3eb5c384-6751-4d50-be23-0c2ccc35593c
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5d74a1e0d0ec8a295792ac71946d46fb673b5082
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="registeroutparameter-method-int-int-javalangstring"></a>Método registerOutParameter (int, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra el parámetro OUT en la posición ordinal especificada para el tipo JDBC y el nombre del tipo especificados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 java.lang.String typeName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica la posición ordinal del parámetro.  
  
 *SQLtype*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
 *TypeName*  
  
 A **cadena** que contiene el nombre de tipo completo de SQL.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método registerOutParameter especificado por el método registerOutParameter de la interfaz java.sql.CallableStatement.  
  
 A partir de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] controlador JDBC 3.0, cuando *sqlType* es de tipo java.sql.Types.TIME, se modifica el comportamiento de este método mediante el **sendTimeAsDatetime** propiedad de conexión ([Estableciendo las propiedades de conexión](../../../connect/jdbc/setting-the-connection-properties.md)) y [SQLServerDataSource.setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md).  
  
 Para obtener más información, consulte [java.sql.Time cómo configurar los valores se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Vea también  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
