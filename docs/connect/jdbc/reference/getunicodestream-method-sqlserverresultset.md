---
title: Método getUnicodeStream (SQLServerResultSet) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.getUnicodeStream
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0dd61865-663b-47e2-b417-e9df418894cc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4eb5989f2674825963f2db2157d67d85416d030
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80910948"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>Método getUnicodeStream (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.  
  
> [!NOTE]  
>  Este método se ha dejado de incluir en las especificaciones de JDBC y si se llama producirá una excepción de no implementación. En su lugar, debería utilizar el método [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|Nombre|Descripción|  
|----------|-----------------|  
|[Método getUnicodeStream &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|Recupera el valor del índice de la columna que se ha designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.|  
|[Método getUnicodeStream &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|Recupera el valor del nombre de la columna que se ha designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.|  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
