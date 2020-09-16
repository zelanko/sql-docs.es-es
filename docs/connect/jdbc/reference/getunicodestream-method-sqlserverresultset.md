---
description: Método getUnicodeStream (SQLServerResultSet)
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
ms.openlocfilehash: 43590c9d660a54d24c42b8032ee886ffcd587ed0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88433917"
---
# <a name="getunicodestream-method-sqlserverresultset"></a>Método getUnicodeStream (SQLServerResultSet)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de la columna designada en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.  
  
> [!NOTE]  
>  Este método se ha dejado de incluir en las especificaciones de JDBC y si se llama producirá una excepción de no implementación. En su lugar, debería utilizar el método [getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md).  
  
## <a name="overload-list"></a>Lista de sobrecargas  
  
|NOMBRE|Descripción|  
|----------|-----------------|  
|[Método getUnicodeStream &#40;int&#41;](../../../connect/jdbc/reference/getunicodestream-method-int.md)|Recupera el valor del índice de la columna que se ha designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.|  
|[Método getUnicodeStream &#40;java.lang.String&#41;](../../../connect/jdbc/reference/getunicodestream-method-java-lang-string.md)|Recupera el valor del nombre de la columna que se ha designado en la fila actual de este objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) como un flujo de caracteres Unicode.|  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
