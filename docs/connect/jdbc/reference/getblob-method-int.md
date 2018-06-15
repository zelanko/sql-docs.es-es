---
title: Método getBlob (int) | Documentos de Microsoft
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
- SQLServerCallableStatement.getBlob (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: bef3ef12-cdda-4a18-90d6-4a501b8e30f0
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1ade0d109f2f20edcd1a6a0ff2aca1e8ba71a00b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32831220"
---
# <a name="getblob-method-int"></a>Método getBlob (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro JDBC BLOB designado como un objeto Blob en el lenguaje de programación Java según el índice del parámetro.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Blob getBlob(int index)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica el índice del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Blob.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getBlob se especifica por getBlob (método) en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método getBlob &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getblob-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
