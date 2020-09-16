---
description: Método cancelRowUpdates (SQLServerResultSet)
title: Método cancelRowUpdates (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.cancelRowUpdates
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 2ecacca4-f7bc-4f5d-886a-da7747fdccae
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 32e5333f571ff9375bdbdc61e9743d29a57cedfd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88438187"
---
# <a name="cancelrowupdates-method-sqlserverresultset"></a>Método cancelRowUpdates (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Cancela las actualizaciones realizadas en la fila actual en este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void cancelRowUpdates()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método cancelRowUpdates especifica este método cancelRowUpdates en la interfaz java.sql.ResultSet.  
  
 Se puede llamar a este método después de llamar a un método updater y antes de llamar al método [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para revertir las actualizaciones realizadas en una fila. Si no se han realizado actualizaciones o ya se ha llamado a updateRow, este método no tendrá efecto alguno.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
