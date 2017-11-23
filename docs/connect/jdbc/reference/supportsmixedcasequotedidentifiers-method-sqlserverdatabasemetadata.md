---
title: "Método supportsMixedCaseQuotedIdentifiers | Documentos de Microsoft"
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
apiname: SQLServerDatabaseMetaData.supportsMixedCaseQuotedIdentifiers
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 76c68fc2-5af6-4b8d-baee-245716fdc5cc
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 80a901d63364a7ebb80f93f2b4ce5655021e8e67
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="supportsmixedcasequotedidentifiers-method-sqlserverdatabasemetadata"></a>Método supportsMixedCaseQuotedIdentifiers (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos trata los identificadores de SQL de mayúsculas y minúsculas mezcladas que están entre comillas como entre mayúsculas y minúsculas y los almacena en mayúsculas y minúsculas mezcladas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsMixedCaseQuotedIdentifiers()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si los identificadores están almacenados en mayúsculas y minúsculas mezcladas. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método supportsMixedCaseQuotedIdentifiers especificado por el método supportsMixedCaseQuotedIdentifiers en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
