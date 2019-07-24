---
title: Método registerOutParameter (int, int, int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter (int, int, int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: d902d4e0-881f-4182-814c-0ede9a8da7fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6948bf6b86160b1752a483b13f83abbfc467ef2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67975942"
---
# <a name="registeroutparameter-method-int-int-int"></a>Método registerOutParameter (int, int, int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra el parámetro OUT en la posición ordinal especificada para el tipo JDBC y escala determinados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void registerOutParameter(int index,  
                                 int sqlType,  
                                 int scale)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Valor **int** que indica la posición ordinal del parámetro.  
  
 *sqlType*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
 *escala*  
  
 Valor **int** que indica el número de dígitos que se van a colocar a la derecha del signo decimal.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método registerOutParameter se especifica mediante el método registerOutParameter de la interfaz java. SQL. CallableStatement.  
  
 Desde el controlador JDBC de 3,0, cuando *sqlType* es de tipo Java. SQL. types. Time, el comportamiento de este método se modifica mediante la propiedad de conexión **sendTimeAsDatetime** ( [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [Establecer las propiedades](../../../connect/jdbc/setting-the-connection-properties.md)de conexión) [y SQLServerDataSource.](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)setSendTimeAsDatetime.  
  
 Para más información, vea [Configurar el modo en que los valores java.sql.Time se envían al servidor](../../../connect/jdbc/configuring-how-java-sql-time-values-are-sent-to-the-server.md).  
  
## <a name="see-also"></a>Consulte también  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
