---
description: Método getTrustServerCertificate (SQLServerDataSource)
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c3a5de057e6a9363f4e3feeace35f2b5105d3cd3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434057"
---
# <a name="gettrustservercertificate-method-sqlserverdatasource"></a>Método getTrustServerCertificate (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **Boolean** que indica si la propiedad trustServerCertificate está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getTrustServerCertificate()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si trustServerCertificate está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 Si la propiedad trustServerCertificate se establece en **true**, se confía automáticamente en el certificado de Seguridad de la capa de transporte (TLS) de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], antes conocida como Capa de sockets seguros (SSL), cuando el nivel de comunicación se cifra mediante SSL. Es decir, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] no validará el certificado TLS/SSL de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor predeterminado es **false**.  
  
 Si la propiedad trustServerCertificate se establece en **false**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] validará el certificado TLS/SSL del servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
