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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: deeab57c573311db36eabdbad60c3cb2fbda9a47
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "67974216"
---
# <a name="sethostnameincertificate-method-sqlserverdatasource"></a>Método setHostNameInCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre de host que se va a utilizar para validar el certificado de Capa de sockets seguros (SSL) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setHostNameInCertificate(java.lang.String hostNameInCertificate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *hostNameInCertificate*  
  
 Objeto **String** que contiene el nombre de host.  
  
## <a name="remarks"></a>Observaciones  
 El valor hostNameInCertificate se utiliza para validar el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el nivel de comunicación se cifra mediante SSL. El valor predeterminado es null.  
  
 Si la propiedad hostNameInCertificate está establecida en NULL o no se ha especificado, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] usará el valor de propiedad serverName para realizar la validación con respecto al certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Si la propiedad hostNameInCertificate está establecida en una cadena o una cadena vacía "", el controlador utilizará ese valor para validar el certificado SSL del servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
