---
title: Método setFetchSize (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 760e555e-9667-4b40-b0ba-778026ff2923
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: acf74ae4b3f9c95002de418a5b77a44a7b0a1bfa
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66764599"
---
# <a name="setfetchsize-method-sqlserverstatement"></a>Método setFetchSize (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ofrece una sugerencia al [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sobre el número de filas que se deben capturar de la base de datos cuando se necesiten más filas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setFetchSize(int rows)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *rows*  
  
 Un valor**int** que indica el número de filas que se van a capturar.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setFetchSize especificado por el método setFetchSize en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
