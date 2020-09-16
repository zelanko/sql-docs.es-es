---
description: Método getPropertyInfo (SQLServerDriver)
title: Método getPropertyInfo (SQLServerDriver) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDriver.getPropertyInfo
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: b5eaad8a-31ef-44ac-af11-d5caa13ac3e2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: cfdcc8917d818ff74d5897e9481f829f1284bdee
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88434927"
---
# <a name="getpropertyinfo-method-sqlserverdriver"></a>Método getPropertyInfo (SQLServerDriver)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se utiliza para detectar las propiedades necesarias para efectuar la conexión a una base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.DriverPropertyInfo[] getPropertyInfo(java.lang.String Url,  
                                                     java.util.Properties Info)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Url*  
  
 Un valor **String** que contiene la dirección URL que se utiliza para conectar a la base de datos.  
  
 *Información*  
  
 Una lista de parejas de valores de propiedad, que producen el valor NULL la primera vez que se utilizan.  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de objetos DriverPropertyInfo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getPropertyInfo especifica este método getPropertyInfo en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
