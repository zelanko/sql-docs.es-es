---
title: Método getNString (java.lang.String) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: b351e999-85bf-498b-915a-f91d89134bce
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d837c3739648ac3f5083a4b01d2edc8a9a9fad93
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32836360"
---
# <a name="getnstring-method-javalangstring"></a>Método getNString (java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el valor de designado **NCHAR**, **NVARCHAR**, o **LONGNVARCHAR** parámetro como una cadena en el Java lenguaje de programación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final java.lang.String getNString(java.lang.String parameterName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *parameterName*  
  
 A **cadena** que contiene el nombre del parámetro.  
  
## <a name="return-value"></a>Valor devuelto  
 AStringobject.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getNString especificado por el método getNString en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Vea también  
 [Método getNString &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/getnstring-method-sqlservercallablestatement.md)   
 [Métodos SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-methods.md)  
  
  
