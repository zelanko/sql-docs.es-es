---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c80123c2cc08d01c4fb41c945954288bb999f897
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47810653"
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
  
## <a name="remarks"></a>Notas  
 Este método cancelRowUpdates especificado por el método cancelRowUpdates en la interfaz java.sql.ResultSet.  
  
 Se puede llamar a este método después de llamar a un método updater y antes de llamar al método [updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md) para revertir las actualizaciones realizadas en una fila. Si no se han realizado actualizaciones o ya se ha llamado a updateRow, este método no tendrá efecto alguno.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
