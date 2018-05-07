---
title: setDateTimeOffset (int, java.sql.DateTimeOffset) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 722250967bca8484f359d1e33a7541d34eb3ac79
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="setdatetimeoffsetint-javasqldatetimeoffset-sqlserverstatement"></a>setDateTimeOffset(int, java.sql.DateTimeOffset) (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado para el valor DateTimeOffset especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setDateTimeOffset(int parameterIndex, DateTimeOffset dateTime)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterIndex*  
  
 Índice de la columna que se va a establecer.  
  
 *DateTimeOffset*  
  
 Un objeto DateTimeOffset.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 El formato de DateTimeOffset es "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Utilice la siguiente tabla a modo de referencia.  
  
|Tipo de SQL|Insert|  
|--------------|------------|  
|datetime|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Solo puede insertar: "AAAA-MM-DD hh:mm:ss"|  
|Time|Solo puede insertar: "hh:mm:ss[.nnnnnnn]"|  
|Date|Solo puede insertar: "AAAA-MM-DD"|  
|datetime2|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Vea también  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
