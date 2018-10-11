---
title: Método rowUpdated (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 40afdf8854e40050e718b9c456eaf0a41f7430b4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47614939"
---
# <a name="rowupdated-method-sqlserverresultset"></a>Método rowUpdated (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se ha actualizado la fila actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si el propietario u otro usuario han actualizado la fila visiblemente y si se detectan actualizaciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método rowUpdated especificado por el método rowUpdated en la interfaz java.sql.ResultSet.  
  
 El valor que se devuelve depende de si el conjunto de resultados puede detectar las actualizaciones o no.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no detecta las filas actualizadas para cualquier tipo de cursor.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
