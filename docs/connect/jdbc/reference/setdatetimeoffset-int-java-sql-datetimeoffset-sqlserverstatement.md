---
title: setDateTimeOffset(int, java.sql.DateTimeOffset) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: e8b6e380-6b53-489b-be73-73fcb5258269
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 36b23fb46e8cd909cf71e696293f2981731a86d2
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66793914"
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
  
 *dateTimeOffset*  
  
 Un objeto DateTimeOffset.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 El formato de DateTimeOffset es "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Utilice la siguiente tabla a modo de referencia.  
  
|Tipo de SQL|Insert|  
|--------------|------------|  
|DATETIME|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Solo puede insertar: "AAAA-MM-DD hh:mm:ss"|  
|Time|Solo puede insertar: "hh:mm:ss[.nnnnnnn]"|  
|date|Solo puede insertar: "AAAA-MM-DD"|  
|datetime2|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Consulte también  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
