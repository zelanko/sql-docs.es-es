---
title: "Método SupportsDataDefinitionAndDataManipulationTransactions | Documentos de Microsoft"
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
- SQLServerDatabaseMetaData.supportsDataDefinitionAndDataManipulationTransactions
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: fe91c601-9bb3-4364-9131-575a94d3a1b3
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ef737ab16ddc2178019bbecf33511cff31f3e497
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="supportsdatadefinitionanddatamanipulationtransactions-method-sqlserverdatabasemetadata"></a>Método supportsDataDefinitionAndDataManipulationTransactions (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite instrucciones de definición y manipulación de datos en una transacción.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsDataDefinitionAndDataManipulationTransactions()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si se admite. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método suportsDataDefinitionAndDataManipulationTransactions especificado por el método suportsDataDefinitionAndDataManipulationTransactions en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
