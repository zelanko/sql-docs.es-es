---
title: "Método setBinaryStream (int, java.io.InputStream) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6c32b904-c44b-472e-a084-38f008a742b4
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3011937144ea46a42bb0b77261c7d3261df91e70
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setbinarystream-method-int-javaioinputstream"></a>Método setBinaryStream (int, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el flujo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setAsciiStream(int parameterIndex,  
                                 java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Un **int** que indica el número de parámetro.  
  
 *x*  
  
 Un objeto java.io.InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setBinaryStream especificado por el método setBinaryStream en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método setBinaryStream &#40; SQLServerPreparedStatement &#41;](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)   
 [Miembros SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-members.md)  
  
  

