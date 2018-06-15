---
title: Método Unwrap (SQLServerStatement) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ce680176-ef04-4e44-bb6c-ec50bd06e7e6
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c0439fe23c859caf5884925f881c5bbc4167c164
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32850480"
---
# <a name="unwrap-method-sqlserverstatement"></a>Método unwrap (SQLServerStatement)
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
 El [unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md) método se define mediante la interfaz java.sql.Wrapper, que se introdujo en las especificaciones de JDBC 4.0.  
  
 Las aplicaciones necesiten tener acceso a las extensiones para la API de JDBC que son específicas de la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. El método unwrap admite la acción de desencapsular para las clases públicas que extiende este objeto, si las clases tienen extensiones de proveedor.  
  
 Cuando se llama a este método, el objeto desencapsula la [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) clase.  
  
 Por ejemplo de código, vea [muestra de datos grandes actualización](../../../connect/jdbc/updating-large-data-sample.md), o [unwrap (método) &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/unwrap-method-sqlservercallablestatement.md).  
  
 Para obtener más información, consulte [contenedores e Interfaces](../../../connect/jdbc/wrappers-and-interfaces.md).  
  
## <a name="see-also"></a>Vea también  
 [Método isWrapperFor &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
