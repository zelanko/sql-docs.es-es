---
title: "Método Unwrap (SQLServerPreparedStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8e3ec950-3ac1-4c28-9e97-ddce3bd46578
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 85f008a4cf1135b1a0978d98bade8d2c99030629
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverpreparedstatement"></a>Método unwrap (SQLServerPreparedStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *iface*  
  
 Una clase de tipo **T** define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto que implementa la interfaz especificada.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 El [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md) método se define mediante la interfaz java.sql.Wrapper, que se introdujo en las especificaciones de JDBC 4.0.  
  
 Las aplicaciones necesiten tener acceso a las extensiones para la API de JDBC que son específicas de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. El método unwrap admite la acción de desencapsular para las clases públicas que extiende este objeto, si las clases tienen extensiones de proveedor.  
  
 Cuando se llama a este método, el objeto desencapsula las siguientes clases: [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) y [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md).  
  
 Por ejemplo de código, vea [unwrap (método) &#40; SQLServerCallableStatement &#41; ](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Método isWrapperFor &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)   
 [Miembros de SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)   
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  
