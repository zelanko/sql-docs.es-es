---
title: setPoolable (método) (SQLServerStatement) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f0f798c8-cafb-4acc-b85d-2e0059c91d92
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9647e2e2c887c95a647a4c5c6b3ca64efcf8c1d3
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setpoolable-method-sqlserverstatement"></a>setPoolable (método) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Solicita que una instrucción se agrupe o no.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setPoolable(boolean poolable) throws SQLException  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Puede agrupar*  
  
 Si **true**, solicita que la instrucción se agrupe. Si **false**, las solicitudes que no se agrupe la instrucción.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 El valor especificado en el *agrupables* parámetro es una sugerencia para la implementación de grupo de la instrucción que indica si la aplicación desea que la instrucción se agrupe. El administrador del grupo de instrucciones decide si va a utilizar la sugerencia.  
  
 El valor del grupo de una instrucción se aplica a las memorias caché de instrucciones internas que implementa el controlador y a las memorias caché de instrucciones externas que implementan los servidores y otras aplicaciones.  
  
 De forma predeterminada, no es puede agrupar cuando se crea un objeto SQLServerStatement. Los objetos SQLServerPreparedStatement y SQLServerCallableStatement son puede agrupables cuando se creó.  
  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md) se produce si se llama a este método en una instrucción cerrada.  
  
 [isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md) devuelve un valor que indica si el objeto se puede agrupar.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
