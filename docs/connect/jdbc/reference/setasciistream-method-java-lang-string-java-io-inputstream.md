---
title: "Método para la secuencia de entrada setAsciiStream | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: dc2caa44-9eb5-4ed8-a889-36148b50901d
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 81607cc031734d8ef361380a36b423286f5557ac
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setasciistream-method-javalangstring-javaioinputstream"></a>Método setAsciiStream (java.lang.String, java.io.InputStream)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el parámetro designado en el flujo de entrada especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setAsciiStream(java.lang.String parameterName,  
                                java.io.InputStream x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
 *x*  
  
 Un objeto InputStream.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setAsciiStream especificado por el método setAsciiStream en la interfaz java.sql.PreparedStatement.  
  
## <a name="see-also"></a>Vea también  
 [setAsciiStream &#40; SQLServerCallableStatement &#41;](../../../connect/jdbc/reference/setasciistream-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)  
  
  
