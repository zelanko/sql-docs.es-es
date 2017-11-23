---
title: Clase SQLServerCallableStatement | Documentos de Microsoft
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
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
caps.latest.revision: "20"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 2fb8757c3bef90d69d8ea1ea9b42720d64eefa7a
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlservercallablestatement-class"></a>Clase SQLServerCallableStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Le permite especificar el nombre del procedimiento almacenado que se va a llamar junto con los parámetros de entrada y salida. Esta clase también proporciona la capacidad de recuperar el valor de estado de retorno con la sintaxis ? = call( ?, ..).  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Implementa:** [ISQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
 **Extiende:** [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final class SQLServerCallableStatement  
```  
  
## <a name="remarks"></a>Comentarios  
 SQLServerCallableStatement le permite especificar el nombre de procedimiento almacenado va a llamar junto con los parámetros de entrada y salidos. SQLServerCallableStatement también proporciona la capacidad para recuperar el valor de estado devuelto con el `? = call( ?, ..)` sintaxis.  
  
 Esta clase admite la acción de desencapsular para la clase SQLServerCallableStatement, ISQLServerCallableStatement, interfaz, la interfaz java.sql.CallableStatement, las clases e interfaces compatibles con SQLServerPreparedStatement para la acción de desencapsular. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Cuando establece uno de la SQLServerCallableStatement métodos se llama para un tipo, si ese tipo entra en conflicto con el tipo especificado con [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), se utiliza el tipo especificado por el último método set de SQLServerCallableStatement. Sin embargo, esto puede producir errores de conversión de tipos de datos incompatibles. Si un SQLServerCallableStatement establece el método no se llama, el tipo especificado con la primera [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md) llamada se usa.  
  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] 3.0 del controlador JDBC es compatible con la recomendación de JDBC 4.0 que un conjunto de resultados y recuentos de actualizaciones se deben recuperar antes de recuperar los parámetros de salida. Si se recuperan los parámetros OUT antes de que se hayan procesado completamente los conjuntos de resultados y las actualizaciones, se perderán todos los conjuntos de resultados y las actualizaciones que no se hayan procesado.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
