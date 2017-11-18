---
title: "Método setHostNameInCertificate (SQLServerDataSource) | Documentos de Microsoft"
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
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a498f6f14a5836637784b98a2f8bf82134f3de61
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Método setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre de host que se usará para validar la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado de capa de Sockets seguros (SSL).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *hostNameInCertificate*  
  
 A **cadena** que contiene el nombre de host.  
  
## <a name="remarks"></a>Comentarios  
 El valor hostNameInCertificate se utiliza para validar la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] este certificado SSL cuando el nivel de comunicación se cifra mediante SSL. El valor predeterminado es null.  
  
 Si la propiedad hostNameInCertificate está establecida en null o no especificado, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará el valor de propiedad serverName para validar con la [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL. Si la propiedad hostNameInCertificate está establecida en una cadena o una cadena vacía "", el controlador utilizará ese valor para validar el certificado SSL del servidor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  

