---
title: Método getTrustManagerConstructorArg (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getTrustManagerConstructorArg
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 24efba087c6e2f988e25517ceffb61463b0ec935
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66786198"
---
# <a name="gettrustmanagerconstructorarg-method-sqlserverdatasource"></a>Método getTrustManagerConstructorArg (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de cadena de la propiedad de conexión de propiedades de conexión.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getTrustManagerConstructorArg()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **cadena** que contiene el valor de la propiedad de conexión de propiedades de conexión, o null si se establece ningún valor.  
  
## <a name="remarks"></a>Notas  
 Si no se establece la propiedad TrustManagerClass, el [getTrustManagerConstructorArg](../../../connect/jdbc/reference/gettrustmanagerconstructorarg-method-sqlserverdatasource.md) método devuelve null.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
