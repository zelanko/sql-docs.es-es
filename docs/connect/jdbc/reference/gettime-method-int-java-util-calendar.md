---
description: Método getTime (int, java.util.Calendar)
title: Método getTime (int, java.util.Calendar) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.getTime (int, java.util.Calendar)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 87b7fbaf-7149-494f-b3b2-16b468a8ebf1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c4db287525eb6752abd9178c44bd16cc0cafe561
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434277"
---
# <a name="gettime-method-int-javautilcalendar"></a>Método getTime (int, java.util.Calendar)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor del parámetro designado como un objeto java.sql.Time en el lenguaje de programación Java según el índice de parámetro y mediante el uso del objeto Calendar determinado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Time getTime(int index,  
                             java.util.Calendar cal)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Un valor **int** que indica el índice del parámetro.  
  
 *cal*  
  
 Un objeto Calendar.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Time.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getTime especifica este método getTime en la interfaz java.sql.CallableStatement.  
  
 Consulte el gráfico titulado "Conversiones de métodos de captador" en [Descripción de las conversiones de tipos de datos](../../../connect/jdbc/understanding-data-type-conversions.md) para ver los tipos datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se pueden recuperar con este método.  
  
## <a name="see-also"></a>Consulte también  
 [Método getTime &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/gettime-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
