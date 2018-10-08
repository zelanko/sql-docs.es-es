---
title: Método getTrustServerCertificate (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- getTrustServerCertificate Method (SQLServerDataSource)
apilocation:
- getTrustServerCertificate Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: e4f443cc-b5d7-4859-81df-836a8642ed07
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 008b0c0263ec73f0f316820c92ba5d70ca286d62
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47745533"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>Método getTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **Boolean** que indica si la propiedad trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si trustServerCertificate está habilitada. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad trustServerCertificate se establece en **true**, se confía automáticamente en el certificado de Capa de sockets seguros (SSL) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cuando el nivel de comunicación se cifra mediante SSL. Es decir, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no validará el certificado SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor predeterminado es **false**.  
  
 Si la propiedad trustServerCertificate se establece en **false**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará el certificado SSL del servidor.  
  
## <a name="see-also"></a>Ver también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
