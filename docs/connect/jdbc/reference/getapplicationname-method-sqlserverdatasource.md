---
title: "Método getApplicationName (SQLServerDataSource) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLServerDataSource.getApplicationName
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: f71e501c-ccd7-4a1e-b6ea-4d47a81c18c6
caps.latest.revision: "13"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 1003b679dc8e34da4196fbfd92bef729a17310ba
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="getapplicationname-method-sqlserverdatasource"></a>Método getApplicationName (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre de la aplicación.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getApplicationName()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre de la aplicación, o "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]" si se establece ningún valor.  
  
## <a name="remarks"></a>Comentarios  
 El nombre de la aplicación se usa para identificar la aplicación específica en diversas [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] de generación de perfiles y herramientas de registro. Si no se establece el nombre de la aplicación, el método getApplicationName devuelve la cadena no localizada "[!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]".  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
