---
title: "Método getPortNumber (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.getPortNumber
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: e5dc38d0-4340-4ad7-a56e-1d2a0f0fd846
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2cf2e36d551a3b9e2e6e990c4945708043277e6a
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getportnumber-method-sqlserverdatasource"></a>Método getPortNumber (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el número de puerto actual que se usa para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public int getPortNumber()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **int** valor que contiene el número de puerto actual.  
  
## <a name="remarks"></a>Comentarios  
 El número de puerto es el número de puerto TCP/IP que se utiliza al abrir una conexión de socket a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Si no se establece la propiedad portNumber, el método getPortNumber devuelve el valor predeterminado de 1433.  
  
> [!NOTE]  
>  El [setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md) método no realiza ninguna comprobación en el valor del puerto pasado del intervalo. Puede pasar números erróneos que no son válidos, como 99999, sin que se desencadene un error.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

