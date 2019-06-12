---
title: Clase SQLServerDataSourceObjectFactory | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b616632b-5987-470d-b36c-b22fa9213145
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 6314bf3fe9f0d5773ed1084858ea1691418528af
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66784360"
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
  
## <a name="remarks"></a>Notas  
 Este método lo heredan todas las clases de orígenes de datos. Como parte de su compatibilidad con la interfaz Referenceable, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] expone esta clase que implementa ObjectFactory. Cuando los servidores de aplicaciones Java llaman a getReference en una clase de origen de datos, se crea un objeto Reference que usa internamente el nombre de la clase como su generador de clases.  
  
 Cuando el servidor de aplicaciones Java tiene que eliminar referencias del objeto de referencia, crea una instancia del objeto SQLServerDataSourceObjectFactory y llama a la [getObjectInstance](../../../connect/jdbc/reference/getobjectinstance-method-sqlserverdatasourceobjectfactory.md) método, pasando el objeto de referencia a recuperar la instancia de origen de datos.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros de SQLServerDataSourceObjectFactory](../../../connect/jdbc/reference/sqlserverdatasourceobjectfactory-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
