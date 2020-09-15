---
description: Método setTrustManagerConstructorArg (SQLServerDataSource)
title: Método setTrustManagerConstructorArg (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setTrustManagerConstructorArg
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8e6ede59019da1870c5a1757ed6d2b082c3736e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88354951"
---
# <a name="settrustmanagerconstructorarg-method-sqlserverdatasource"></a>Método setTrustManagerConstructorArg (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el valor de cadena de la propiedad de conexión TrustManagerConstructorArg.
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setTrustManagerConstructorArg(java.lang.String trustManagerClass)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *trustManagerClass*  
  
 Un valor de **cadena** que contiene el nombre de clase completo de custom javax.net.ssl.TrustManager.
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
