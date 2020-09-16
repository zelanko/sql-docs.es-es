---
description: Método registerOutParameter (java.lang.String, int, java.lang.String)
title: Método registerOutParameter para tipo y nombre | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerCallableStatement.registerOutParameter
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: f962c912-2475-4e1f-a384-579be2d17f37
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 0fab9ba4e979780fedfb676fd779f8ed83da7566
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88432807"
---
# <a name="registeroutparameter-method-javalangstring-int-javalangstring"></a>Método registerOutParameter (java.lang.String, int, java.lang.String)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Registra el parámetro OUT con el nombre especificado para el nombre de tipo y el tipo JDBC dado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void registerOutParameter(java.lang.String s,  
                                 int n,  
                                 java.lang.String s1)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *s*  
  
 Objeto **String** que contiene el nombre del parámetro.  
  
 *n*  
  
 Un código de tipo JDBC tal como se define en java.sql.Types.  
  
 *s1*  
  
 Objeto **String** que contiene el nombre del tipo SQL completo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método registerOutParameter especifica este método registerOutParameter en la interfaz java.sql.CallableStatement.  
  
## <a name="see-also"></a>Consulte también  
 [Método registerOutParameter &#40;SQLServerCallableStatement&#41;](../../../connect/jdbc/reference/registeroutparameter-method-sqlservercallablestatement.md)   
 [Miembros SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-members.md)   
 [Clase SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md)  
  
  
