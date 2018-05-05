---
title: rowUpdated (método) (SQLServerResultSet) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerResultSet.rowUpdated
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 29303550-294e-4d43-b892-312b42e21271
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 37b981097aa6140e892997ce11ccd5ca98567e87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="rowupdated-method-sqlserverresultset"></a>rowUpdated (método) (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si se ha actualizado la fila actual.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean rowUpdated()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si tanto la fila se ha actualizado visiblemente por el propietario o de otro usuario, y se detectan las actualizaciones. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método rowUpdated es especificado por el método rowUpdated en la interfaz java.sql.ResultSet.  
  
 El valor que se devuelve depende de si el conjunto de resultados puede detectar las actualizaciones o no.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] no detecta las filas actualizadas para cualquier tipo de cursor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
