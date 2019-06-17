---
title: Método setFetchDirection (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4ee82290-508d-4bff-a5c5-8a56338deef8
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 31315b70f770d2f95e97d34b2064152234cae248
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66803395"
---
# <a name="setfetchdirection-method-sqlserverresultset"></a>Método setFetchDirection (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ofrece una sugerencia sobre la dirección en la que se procesarán las filas de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md).  
  
> [!NOTE]  
>  El [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no admite este método actualmente. Si utiliza este método, el controlador JDBC recuerda la configuración, pero no emprende ninguna acción con el método por el momento.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setFetchDirection(int direction)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *direction*  
  
 Un valor **int** que indica la dirección de recuperación sugerida. Puede ser uno de los siguientes valores:  
  
 ResultSet.FETCH_FORWARD  
  
 ResultSet.FETCH_REVERSE  
  
 ResultSet.FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método setFetchDirection especificado por el método setFetchDirection en la interfaz java.sql.ResultSet.  
  
 El valor inicial de este método lo determina el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que ha generado este objeto SQLServerResultSet. La dirección de la captura puede cambiar en cualquier momento.  
  
> [!NOTE]  
>  Si se utiliza este método cuando el tipo de cursor es de solo avance, no tendrá efecto alguno.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
