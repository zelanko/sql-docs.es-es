---
title: Método setTrustServerCertificate (SQLServerDataSource) | Documentos de Microsoft
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
- setTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- setTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 6c37b518-147e-4cd9-9eff-b48a3f5888c6
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb5923c3078944a446abfc763c76122f44af2396
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32845710"
---
# <a name="settrustservercertificate-method-sqlserverdatasource"></a>Método setTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un **booleano** valor que indica si la propiedad trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTrustServerCertificate(boolean trustServerCertificate)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *TrustServerCertificate*  
  
 **True** si el certificado de capa de Sockets seguros (SSL) de servidor debe ser de confianza automáticamente cuando el nivel de comunicación se cifra mediante SSL. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Comentarios  
 Si la propiedad trustServerCertificate se establece en **true**, el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL se confía automáticamente cuando el nivel de comunicación se cifra mediante SSL. En otras palabras, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no validará el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] certificado SSL. El valor predeterminado es **false**.  
  
 Si la propiedad trustServerCertificate se establece en **false**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará el certificado SSL de servidor.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
