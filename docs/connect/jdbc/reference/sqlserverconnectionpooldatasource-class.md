---
title: Clase SQLServerConnectionPoolDataSource | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: b00e5a90-2af7-4d04-8ef8-256183777dcf
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0accd21f53a4ba1a86e4b7555be9d2ba9a087474
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80921046"
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
  
## <a name="remarks"></a>Observaciones  
 SQLServerConnectionPoolDataSource se utiliza normalmente en entornos de servidores de aplicación Java que admiten la agrupación de conexiones integradas y requieren ConnectionPoolDataSource para proporcionar conexiones físicas, como Java Platform, servidores de aplicación de Enterprise Edition (Java EE) que proporcionen agrupaciones de conexiones de las especificaciones de la API de JDBC 3.0.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
