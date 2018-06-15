---
title: Método getHostNameInCertificate (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd5ba2b9a98fedc7d2ebf47c3282cca839d59265
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32835350"
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
  
  
