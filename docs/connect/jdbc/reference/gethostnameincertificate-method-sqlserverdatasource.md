---
title: Método getHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- getHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 45ea04e2-9ea5-4171-9136-d09f8a95e128
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 1bdd2e849654c78fab2fdff8b409c204a1298834
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66774480"
---
# <a name="gethostnameincertificate-method-sqlserverdatasource"></a>Método getHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre del host que se utiliza para validar el certificado de Capa de sockets seguros (SSL) de SQL Server.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getHostNameInCertificate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto **String** que contiene el nombre de host o el valor NULL si no se establece ningún valor.  
  
## <a name="remarks"></a>Notas  
 El nombre de host se utiliza para validar el valor del certificado SSL de SQL cuando el nivel de comunicación se cifra mediante SSL.  
  
 Si no se establece el nombre de host, el método [getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md) devuelve el valor NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
