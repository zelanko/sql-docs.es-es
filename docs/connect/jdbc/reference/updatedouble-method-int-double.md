---
description: Método updateDouble (int, double)
title: Método updateDouble (int, Double) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerResultSet.updateDouble (int, double)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 90c47643-e27e-425d-85a0-63866f858367
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d83a51b8c344f0472b402eb47999e3736384241
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88353491"
---
# <a name="updatedouble-method-int-double"></a>Método updateDouble (int, double)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Actualiza la columna designada con un valor de **double** según el índice de la columna.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void updateDouble(int index,  
                         double x)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *índice*  
  
 Valor **int** que indica el índice de la columna.  
  
 *x*  
  
 Un valor **double**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 Este método updateDouble se especifica mediante el método updateDouble de la interfaz java.sql.ResultSet.  
  
## <a name="see-also"></a>Consulte también  
 [Método updateDouble &#40;SQLServerResultSet&#41;](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)   
 [Miembros SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-members.md)   
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
