---
title: Clase SQLServerCallableStatement | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: 30710a63-c05d-47d9-9cf9-c087a1c76373
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 38d85e88e8095cc5e2f41af045c36f230fbd43de
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810163"
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
  
## <a name="remarks"></a>Notas  
 SQLServerCallableStatement permite especificar el nombre del procedimiento almacenado que se va a llamar junto con los parámetros de entrada y salida. SQLServerCallableStatement también proporciona la capacidad para recuperar el valor de estado de retorno con la `? = call( ?, ..)` sintaxis.  
  
 Esta clase admite la acción de desencapsular para la clase SQLServerCallableStatement, interfaz ISQLServerCallableStatement, interfaz java.sql.CallableStatement, las clases e interfaces compatibles con SQLServerPreparedStatement para la acción de desencapsular. Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Cuando establece uno de la SQLServerCallableStatement métodos se llama para un tipo, si ese tipo entra en conflicto con el tipo especificado con [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), se usa el tipo especificado por el último método set de SQLServerCallableStatement. Sin embargo, esto puede producir errores de conversión de tipos de datos incompatibles. Si no se llama a un método set de SQLServerCallableStatement, se usará el tipo especificado con la primera llamada a [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md).  
  
 El controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sigue la especificación de JDBC 4.0, que indica que se deben recuperar varios conjuntos de resultados y actualizaciones antes de que se recuperen parámetros OUT. Si se recuperan los parámetros OUT antes de que se hayan procesado completamente los conjuntos de resultados y las actualizaciones, se perderán todos los conjuntos de resultados y las actualizaciones que no se hayan procesado.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
