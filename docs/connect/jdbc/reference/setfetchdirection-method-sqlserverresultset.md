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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6f0055facd8248816da07fea74e8dc8035f78d84
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922354"
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
  
## <a name="remarks"></a>Observaciones  
 El método setFetchDirection especifica este método setFetchDirection en la interfaz java.sql.ResultSet.  
  
 El valor inicial de este método lo determina el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) que ha generado este objeto SQLServerResultSet. La dirección de la captura puede cambiar en cualquier momento.  
  
> [!NOTE]  
>  Si se utiliza este método cuando el tipo de cursor es de solo avance, no tendrá efecto alguno.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
