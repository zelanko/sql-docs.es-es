---
title: "Método getPropertyInfo (SQLServerDriver) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 08e0490f891f9423f57067512013d19e81aed68f
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>Método getPropertyInfo (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se utiliza para detectar las propiedades necesarias para efectuar la conexión a una base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Dirección URL*  
  
 A **cadena** valor que contiene la dirección URL que se utiliza para conectarse a la base de datos.  
  
 *Información de*  
  
 Una lista de parejas de valores de propiedad, que producen el valor NULL la primera vez que se utilizan.  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de objetos de DriverPropertyInfo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getPropertyInfo es especificado por el método getPropertyInfo en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Vea también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  

