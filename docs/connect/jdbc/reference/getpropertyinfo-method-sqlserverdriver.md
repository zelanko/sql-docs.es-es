---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 889f530496dd5fa975822702282cc78b99197318
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47624853"
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
  
 *Info*  
  
 Una lista de parejas de valores de propiedad, que producen el valor NULL la primera vez que se utilizan.  
  
## <a name="return-value"></a>Valor devuelto  
 Una matriz de objetos DriverPropertyInfo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getPropertyInfo especificado por el método getPropertyInfo en la interfaz java.sql.Driver.  
  
## <a name="see-also"></a>Ver también  
 [Métodos SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-methods.md)   
 [Miembros de SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-members.md)   
 [Clase SQLServerDriver](../../../connect/jdbc/reference/sqlserverdriver-class.md)  
  
  
