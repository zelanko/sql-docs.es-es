---
title: getCharacterStream (java.lang.String) | Documentos de Microsoft
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
- SQLServerCallableStatement.getCharacterStream(String paramName)
apilocation:
- SQLServerCallableStatement.getCharacterStream(String paramName)
apitype: Assembly
ms.assetid: 5281e1b8-19b8-4fe5-83be-929d1987e25d
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4d1c9c077991f614a04787b48824ead209e1f433
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831010"
---
# <a name="getcharacterstream-javalangstring"></a>getCharacterStream (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.io.Reader según el nombre del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.io.Reader getCharacterStream(java.lang.String paramName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *paramName*  
  
 A **cadena** que indica el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de lector.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="see-also"></a>Vea también  
 [Método getCharacterStream &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getcharacterstream-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
