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
ms.openlocfilehash: 567f5e7e3aca87b875e4f93c26d7caa5535a8c75
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "67978604"
---
# <a name="gettrustmanagerclass-method-sqlserverdatasource"></a>Método getTrustManagerClass (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de String de la propiedad de conexión TrustManagerClass.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getTrustManagerClass()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto **String** que contiene el valor de la propiedad de conexión TrustManagerClass, o null si no se establece ningún valor.  
  
## <a name="remarks"></a>Observaciones  
 Si no se establece la propiedad TrustManagerClass, el método [getTrustManagerClass](../../../connect/jdbc/reference/gettrustmanagerclass-method-sqlserverdatasource.md) devuelve NULL.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
