---
title: "Método getObjectInstance (SQLServerDataSourceObjectFactory) | Documentos de Microsoft"
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
apiname: SQLServerDataSourceObjectFactory.getObjectInstance
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: aa9417d9b20ae5c1858c3c8f10019383565c4330
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getobjectinstance-method-sqlserverdatasourceobjectfactory"></a>Método getObjectInstance (SQLServerDataSourceObjectFactory)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una instancia del objeto de origen de datos especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.Object getObjectInstance(java.lang.Object ref,  
                                          javax.naming.Name name,  
                                          javax.naming.Context c,  
                                          java.util.Hashtable h)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *ref*  
  
 Un **objeto** valor.  
  
 *Nombre*  
  
 Nombre del objeto.  
  
 *c*  
  
 Contexto relativo al nombre especificado.  
  
 *h*  
  
 Entorno que se utiliza para crear el objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Un **objeto** valor.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Comentarios  
 Este método getObjectInstance especificado por el método getObjectInstance en la interfaz javax.naming.spi.ObjectFactory.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [Miembros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Clase SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
