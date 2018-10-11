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
manager: craigg
ms.openlocfilehash: f3c6e0080f4d94b0d792c1994695c590fd4fed66
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47812343"
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
  
## <a name="remarks"></a>Notas  
 Este método setFetchDirection especificado por el método setFetchDirection en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
