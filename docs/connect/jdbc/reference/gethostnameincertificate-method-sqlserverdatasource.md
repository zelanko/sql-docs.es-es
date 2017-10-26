---
title: "Método getHostNameInCertificate (SQLServerDataSource) | Documentos de Microsoft"
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
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d74305f9c389da375a26bf0516f577939b50f7e9
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Método getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre del host que se utiliza para validar el certificado de Capa de sockets seguros (SSL) de SQL Server.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el host del nombre, o null si no se establece ningún valor.  
  
## <a name="remarks"></a>Comentarios  
 El nombre de host se utiliza para validar el valor del certificado SSL de SQL cuando el nivel de comunicación se cifra mediante SSL.  
  
 Si no se establece el nombre de host, el [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) método devuelve null.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

