---
title: Método setHostNameInCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setHostNameInCertificate Method (SQLServerDataSource)
apilocation:
- setHostNameInCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 2bcf4f2e-a103-4374-abc4-ffad4ce8e3c0
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 418e9aea8d44d3be23bc21c5a8950c5788e7c07a
ms.sourcegitcommit: 54cfeb36c9caa51ec68fa8f4a1918e305db5e00a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/11/2020
ms.locfileid: "81219305"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Método setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre del host que se va a usar para validar el certificado de Seguridad de la capa de transporte (TLS) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], antes conocida como Capa de sockets seguros (SSL).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *hostNameInCertificate*  
  
 Objeto **String** que contiene el nombre de host.  
  
## <a name="remarks"></a>Observaciones  
 El valor hostNameInCertificate se usa para validar el certificado TLS/SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el nivel de comunicación se cifra mediante TLS. El valor predeterminado es null.  
  
 Si la propiedad hostNameInCertificate está establecida en NULL o no se ha especificado, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará el valor de propiedad serverName para realizar la validación con respecto al certificado TLS/SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si la propiedad hostNameInCertificate está establecida en una cadena o en una cadena vacía (""), el controlador usará ese valor para validar el certificado TLS/SSL del servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
