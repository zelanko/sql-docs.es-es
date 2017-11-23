---
title: getCharacterStream (int) | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerCallableStatement.getCharacterStream(int paramIndex)
apilocation: SQLServerCallableStatement.getCharacterStream(int paramIndex)
apitype: Assembly
ms.assetid: eb20714b-52bc-4b6c-b23f-c9c3c9d73783
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e4b54bfab96d11d8e205afd8abd0ba61ac980aae
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getcharacterstream-int"></a>getCharacterStream (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.io.Reader según el índice del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.io.Reader getCharacterStream(int paramIndex)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *paramIndex*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Método getCharacterStream &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
