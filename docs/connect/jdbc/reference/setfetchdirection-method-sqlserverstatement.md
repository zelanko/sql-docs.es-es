---
title: Método setFetchDirection (SQLServerStatement) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.setFetchDirection
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 18176517-2fb3-4266-924d-0f01253083d2
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 995f3f0f63728d397cf51013bd5429943e9cac0c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974396"
---
# <a name="setfetchdirection-method-sqlserverstatement"></a>Método setFetchDirection (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Ofrece una sugerencia al [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] sobre la dirección en la que se deben procesar las filas del conjunto de resultados.  
  
> [!NOTE]  
>  Actualmente, el controlador JDBC omite la sugerencia que proporcionada este método.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setFetchDirection(int nDir)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *nDir*  
  
 Un valor **int** que indica la dirección de procesamiento de las filas, que puede ser uno de los valores siguientes:  
  
 FETCH_FORWARD  
  
 FETCH_REVERSE  
  
 FETCH_UNKNOWN  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método setFetchDirection especifica este método setFetchDirection en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
