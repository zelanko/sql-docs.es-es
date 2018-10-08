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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b99e2f6f7bc289e123c36e3a528ec937e0f5f7ec
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47605613"
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
  
## <a name="remarks"></a>Notas  
 Este método rowDeleted especificado por el método rowDeleted en la interfaz java.sql.ResultSet.  
  
 Si se elimina una fila, podría quedar un hueco visible en un conjunto de resultados. Este método se puede utilizar para detectar los huecos en un conjunto de resultados. El valor que se devuelve depende de si este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) puede detectar eliminaciones.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] detecta las filas eliminadas para todos los tipos de cursor actualizable, aunque la detección es transitoria para los cursores dinámicos y hacia delante.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
