---
title: Método setTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 93feffdb0135e4530b43a6f092c581d145b5c0c6
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66783526"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Método setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un valor **Boolean** que indica si la propiedad trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *trustServerCertificate*  
  
 **True** si el certificado de capa de Sockets seguros (SSL) de servidor debe ser de confianza automáticamente cuando el nivel de comunicación se cifra mediante SSL. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad trustServerCertificate se establece en **true**, se confía automáticamente en el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el nivel de comunicación está cifrado con SSL. Es decir, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no validará el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor predeterminado es **false**.  
  
 Si la propiedad trustServerCertificate se establece en **false**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará el certificado SSL del servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
