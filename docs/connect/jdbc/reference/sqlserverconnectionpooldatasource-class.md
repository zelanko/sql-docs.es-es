---
title: Clase SQLServerConnectionPoolDataSource | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fdbe0150749782416eda8d713224df097a68f43a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845910"
---
# <a name="sqlserverconnectionpooldatasource-class"></a>Clase SQLServerConnectionPoolDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa las conexiones a bases de datos físicas para los administradores de grupos de conexiones.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
 **Implementa:** javax.sql.ConnectionPoolDataSource  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerConnectionPoolDataSource  
```  
  
## <a name="remarks"></a>Comentarios  
 SQLServerConnectionPoolDataSource se utiliza normalmente en entornos de servidor de aplicaciones Java que admiten la agrupación de conexiones integradas y requieren un ConnectionPoolDataSource proporcionar conexiones físicas, como Java Platform, Enterprise Edition (Java Los servidores de aplicaciones EE) que proporcionan las API de JDBC 3.0 de especificaciones agrupación de conexiones.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
