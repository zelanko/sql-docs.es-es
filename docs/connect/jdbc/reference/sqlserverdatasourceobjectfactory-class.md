---
title: Clase SQLServerDataSourceObjectFactory | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 19f81b3a458ac0fa2d5e276858fcff45eeb0eb4b
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverdatasourceobjectfactory-class"></a>Clase SQLServerDataSourceObjectFactory
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa un servicio de generación de objetos para materializar los orígenes de datos de la interfaz Java Naming and Directory Interface (JNDI).  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.lang.Object  
  
 **Implementa:** javax.naming.spi.ObjectFactory  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerDataSourceObjectFactory  
```  
  
## <a name="remarks"></a>Comentarios  
 Este método lo heredan todas las clases de orígenes de datos. Como parte de su compatibilidad con la interfaz Referenceable, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] expone esta clase que implementa un ObjectFactory. Servidores de aplicaciones Java llamará getReference en una clase de origen de datos, y esto creará un objeto de referencia que utiliza internamente el nombre de clase como el generador de clases.  
  
 Cuando el servidor de aplicaciones Java tenga que eliminar referencias del objeto de referencia, crea una instancia del objeto SQLServerDataSourceObjectFactory y las llamadas del [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) método, pasando el objeto de referencia, a recuperar la instancia de origen de datos.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
