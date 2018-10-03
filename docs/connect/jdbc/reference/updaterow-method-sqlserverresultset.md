---
title: Método updateRow (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- MSQLServerResultSet.updateRow
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: cfced0ca-a281-40dc-8d2f-370d5f0bf12b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d0a88a70cc6ed4b6bf1df83eb00806714324b0e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47783023"
---
# <a name="updaterow-method-sqlserverresultset"></a>Método updateRow (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la base de datos subyacente con el nuevo contenido de la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateRow()  
```  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método updateRow especificado por el método updateRow en la interfaz java.sql.ResultSet.  
  
 No se puede llamar a este método cuando el cursor está en la fila de inserción.  
  
 Si se llama a este método cuando no se ha modificado ningún valor de columna, se producirá una excepción.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
