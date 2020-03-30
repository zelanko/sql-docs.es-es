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
ms.openlocfilehash: 166c9ddbd4b5c11b3c032a5a4ecf43c95f183473
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974531"
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
  
## <a name="remarks"></a>Observaciones  
 El formato de DateTimeOffset es "AAAA-MM-DD HH-MM-SS[.nnnnnnn] [+][-] HH:MM". Utilice la siguiente tabla a modo de referencia.  
  
|Tipo de SQL|Insertar|  
|--------------|------------|  
|datetime|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnn]"|  
|smalldatetime|Solo puede insertar: "AAAA-MM-DD hh:mm:ss"|  
|Time|Solo puede insertar: "hh:mm:ss[.nnnnnnn]"|  
|Date|Solo puede insertar: "AAAA-MM-DD"|  
|DateTime2|Solo puede insertar: "AAAA-MM-DD hh:mm:ss[.nnnnnnn]"|  
  
## <a name="see-also"></a>Consulte también  
 [getDateTimeOffset &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
