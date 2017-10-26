---
title: "Método Unwrap (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: eb8abe29-f3ec-4752-a590-1d5dc3e48f08
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 6c7fd1ebcd5f1a9a1d963298212b2423f90e194d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="unwrap-method-sqlserverdatasource"></a>Método unwrap (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public <T> T unwrap(Class<T> iface)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *iface*  
  
 Una clase de tipo T que define una interfaz.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto que implementa la interfaz especificada.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 El [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md) método se define mediante la interfaz java.sql.Wrapper, que se introdujo en las especificaciones de JDBC 4.0.  
  
 Las aplicaciones necesiten tener acceso a las extensiones para la API de JDBC que son específicas de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. El método unwrap admite la acción de desencapsular para las clases públicas que amplía este objeto, si las clases tienen extensiones de proveedor.  
  
 Cuando se llama a este método, el objeto desencapsula la [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) clase.  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Método isWrapperFor &#40; SQLServerDataSource &#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)   
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

