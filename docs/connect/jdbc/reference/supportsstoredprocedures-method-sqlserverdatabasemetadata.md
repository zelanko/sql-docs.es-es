---
title: "Método supportsStoredProcedures | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDatabaseMetaData.supportsStoredProcedures
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 776ff53a-8bf3-4864-a7b7-170fdef1a87b
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 318efad9ba2bda192d668f6aa3b4cabfc1fb464e
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="supportsstoredprocedures-method-sqlserverdatabasemetadata"></a>Método supportsStoredProcedures (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite llamadas a procedimientos almacenados que utilicen sintaxis de escape para procedimientos almacenados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsStoredProcedures()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método supportsStoredProcedures especificado por el método supportsStoredProcedures en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  

