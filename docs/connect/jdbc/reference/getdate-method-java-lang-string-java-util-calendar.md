---
description: Método getDate (java.lang.String, java.util.Calendar)
title: Parámetro del método getDate (java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getDate (java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6d0deaf2-6f12-4a6e-b537-a51fa3478059
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 91dec8348bc51894674074c58a7aa5b0c756b8d7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436367"
---
# <a name="getdate-method-javalangstring-javautilcalendar"></a>Método getDate (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Date en el lenguaje de programación Java según el nombre de parámetro y el objeto Calendar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Date getDate(java.lang.String sCol,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *sCol*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *cal*  
  
 Un objeto Calendar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Date.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getDate especifica este método getDate en la interfaz java.sql.CallableStatement.  
  
 Este método devuelve una fecha válida que forma parte de un tipo de datos datetime o smalldatetime de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], con la parte correspondiente a la hora establecida en la hora de inicio de Java de 00:00 (media noche).  
  
## <a name="see-also"></a>Consulte también  
 [Método getDate &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getdate-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
