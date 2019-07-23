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
ms.openlocfilehash: 637b56c7f64d35501be0efef30e8f2a055b5be4b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67971913"
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
 SQLServerCallableStatement permite especificar el nombre del procedimiento almacenado que se va a llamar junto con los parámetros de entrada y salida. SQLServerCallableStatement también proporciona la capacidad de recuperar el valor de estado de retorno `? = call( ?, ..)` con la sintaxis.  
  
 Esta clase admite la desencapsulación en la clase SQLServerCallableStatement, la interfaz ISQLServerCallableStatement, la interfaz java. SQL. CallableStatement y las clases e interfaces que admite SQLServerPreparedStatement para desempaquetar. Para obtener más información, vea [contenedores e interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
 Cuando se llama a uno de los métodos set de SQLServerCallableStatement para un tipo, si ese tipo entra en conflicto con el tipo especificado con [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md), se usa el tipo especificado por el último método Set SQLServerCallableStatement. Sin embargo, esto puede producir errores de conversión de tipos de datos incompatibles. Si no se llama a un método set de SQLServerCallableStatement, se usará el tipo especificado con la primera llamada a [registerOutParameter](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md).  
  
 El controlador JDBC 3.0 de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sigue la especificación de JDBC 4.0, que indica que se deben recuperar varios conjuntos de resultados y actualizaciones antes de que se recuperen parámetros OUT. Si se recuperan los parámetros OUT antes de que se hayan procesado completamente los conjuntos de resultados y las actualizaciones, se perderán todos los conjuntos de resultados y las actualizaciones que no se hayan procesado.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
