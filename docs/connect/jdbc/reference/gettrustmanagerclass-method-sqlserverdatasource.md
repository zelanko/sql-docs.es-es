---
title: Método getTrustManagerClass (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getTrustManagerClass
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 327dcad497c934c787d509a41f0068691bf5588a
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786215"
---
# <a name="gettrustmanagerclass-method-sqlserverdatasource"></a>Método getTrustManagerClass (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de cadena de la propiedad de conexión TrustManagerClass.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getTrustManagerClass()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **cadena** que contiene el valor de la propiedad de conexión de TrustManagerClass, o null si se establece ningún valor.  
  
## <a name="remarks"></a>Notas  
 Si no se establece la propiedad TrustManagerClass, el [getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md) método devuelve null.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
