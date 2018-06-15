---
title: Método getDate (int, java.util.Calendar) | Documentos de Microsoft
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
- SQLServerCallableStatement.getDate (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 38ce7b75-2623-4eff-bc18-8cf7193adec8
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2cdf89172da4d3b0d465a3eae452922e5a5a4877
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32834960"
---
# <a name="getdate-method-int-javautilcalendar"></a>Método getDate (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Date en el lenguaje de programación Java según el índice del parámetro y el objeto de calendario.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Date getDate(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *index*  
  
 Un **int** que indica el índice del parámetro.  
  
 *CAL*  
  
 Un objeto de calendario.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto de fecha.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getDate es especificado por el método getDate en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve una parte de fecha válida de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] **datetime** o **smalldatetime** tipo de datos, con la parte de hora establecida en la hora de inicio de Java de 00:00 (medianoche).  
  
## <a name="see-also"></a>Vea también  
 [Método getDate &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Miembros de SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
