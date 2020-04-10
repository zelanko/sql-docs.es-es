---
title: Método rowDeleted (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowDeleted
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9c6db315-e614-4604-b020-41af6a214cc1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d4f761f4780b2fdb5da210db5bfb38d2368d865f
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80903941"
---
# <a name="rowdeleted-method-sqlserverresultset"></a>Método rowDeleted (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se ha eliminado una fila.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowDeleted()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si se eliminó una fila y se detectaron eliminaciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método rowDeleted especifica este método rowDeleted en la interfaz java.sql.ResultSet.  
  
 Si se elimina una fila, podría quedar un hueco visible en un conjunto de resultados. Este método se puede utilizar para detectar los huecos en un conjunto de resultados. El valor que se devuelve depende de si este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) puede detectar eliminaciones.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecta las filas eliminadas para todos los tipos de cursor actualizables, aunque la detección sea transitoria para los cursores de avance y dinámicos.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
