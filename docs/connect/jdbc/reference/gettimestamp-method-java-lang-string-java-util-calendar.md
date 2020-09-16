---
description: Método getTimestamp (java.lang.String, java.util.Calendar)
title: Método getTimestamp (java.lang.String, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTimestamp (java.lang.String,java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 770668d9-2e52-4ff0-be2f-ebf78fd41644
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e4a6248c2c14ca93604b5da2f5f28461aa601a03
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434087"
---
# <a name="gettimestamp-method-javalangstring-javautilcalendar"></a>Método getTimestamp (java.lang.String, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Timestamp en el lenguaje de programación Java, según el nombre de parámetro y usando un objeto Calendar.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Timestamp getTimestamp(java.lang.String name,  
                                       java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *name*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *cal*  
  
 Un objeto Calendar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Timestamp.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTimestamp especifica este método getTimestamp en la interfaz java.sql.CallableStatement.  
  
 Este método solamente devuelve valores de columnas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **datetime** y **smalldatetime**.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTimestamp &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettimestamp-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
