---
title: "Método setServerName (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerDataSource.setServerName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 70920828-eda0-4064-be9f-c1e460db8f00
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2efdbb68c0d546776b7027c9130e7589c92322ea
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setservername-method-sqlserverdatasource"></a>Método setServerName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setServerName(java.lang.String serverName)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *serverName*  
  
 A **cadena** que contiene el nombre del servidor.  
  
## <a name="remarks"></a>Comentarios  
 El nombre del servidor es el nombre de host del equipo de destino que se está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)]. Si no se establece la propiedad serverName, [getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md) devuelve el valor predeterminado es null.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
