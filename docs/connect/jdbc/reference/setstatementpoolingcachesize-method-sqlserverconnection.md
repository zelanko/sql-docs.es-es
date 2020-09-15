---
description: Método setStatementPoolingCacheSize (SQLServerConnection)
title: Método setStatementPoolingCacheSize (SQLServerConnection) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection.setStatementPoolingCacheSize
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c14abd6c5251883d348f56d4a1f37d7bb8512f72
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88355291"
---
# <a name="setstatementpoolingcachesize-method-sqlserverconnection"></a>Método setStatementPoolingCacheSize (SQLServerConnection)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

 Establece el tamaño de la memoria caché de instrucciones preparadas para esta conexión. Funciona si disableStatementPooling se establece en false y un valor > 0.

## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setStatementPoolingCacheSize(int statementPoolingCacheSize)  
```  

#### <a name="parameters"></a>Parámetros  
 *statementPoolingCacheSize*  
  
 Nuevo valor de la propiedad de conexión **statementPoolingCacheSize**.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Observaciones  
 Este método está disponible en la versión 6.4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-members.md)   
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  
