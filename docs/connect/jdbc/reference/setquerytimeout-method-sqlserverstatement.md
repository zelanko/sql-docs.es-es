---
title: Método setQueryTimeout (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setQueryTimeout
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0c513265-cd0c-4b38-9494-94458c17a16d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 050a32c83950d2846ac60d14af0413f0be67110d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80920744"
---
# <a name="setquerytimeout-method-sqlserverstatement"></a>Método setQueryTimeout (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el número de segundos que esperará el controlador antes de que se ejecute un objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) según el número de segundos determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setQueryTimeout(int seconds)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *segundos*  
  
 Un valor **int** que indica el número de segundos que transcurrirán; se establece en 0 si no hay límite alguno.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setQueryTimeout especifica este método setQueryTimeout en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
