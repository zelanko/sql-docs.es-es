---
title: Método getObjectInstance (SQLServerDataSourceObjectFactory) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSourceObjectFactory.getObjectInstance
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0a1503e2-e991-4d70-a223-087fc63baf73
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: aab186f41d494e9bddf7885ddf7d9f7b3ff65972
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47849513"
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
  
 Valor **Object**.  
  
 *Nombre*  
  
 Nombre del objeto.  
  
 *c*  
  
 Contexto relativo al nombre especificado.  
  
 *h*  
  
 Entorno que se utiliza para crear el objeto.  
  
## <a name="return-value"></a>Valor devuelto  
 Valor **Object**.  
  
## <a name="exceptions"></a>Excepciones  
 java.sql.SQLException  
  
## <a name="remarks"></a>Notas  
 Este método getObjectInstance especificado por el método getObjectInstance en la interfaz javax.naming.spi.ObjectFactory.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-methods.md)   
 [Miembros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Clase SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-class.md)  
  
  
