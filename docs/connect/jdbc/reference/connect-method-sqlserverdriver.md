---
title: Método connect (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.connect
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 43813a4c-1cc7-4659-ba27-f1786f1371eb
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a182f62796d70fe50f646f39d1afb7058d46fd8
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80927727"
---
# <a name="connect-method-sqlserverdriver"></a>Método connect (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Realiza una conexión a la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.Connection connect(java.lang.String Url,  
                                   java.util.Properties suppliedProperties)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Url*  
  
 Un valor **String** que contiene la dirección URL que se utiliza para conectar a la base de datos.  
  
 *suppliedProperties*  
  
 Un conjunto de parejas de valores de cadena que se utiliza como argumentos de conexión.  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto Connection.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método connect especifica este método connect en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
