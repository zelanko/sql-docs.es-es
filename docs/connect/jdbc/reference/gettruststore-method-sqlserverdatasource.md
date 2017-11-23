---
title: "Método getTrustStore (SQLServerDataSource) | Documentos de Microsoft"
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
apiname: getTrustStore Method (SQLServerDataSource)
apilocation: getTrustStore Method (SQLServerDataSource)
apitype: Assembly
ms.assetid: 8f5850e4-8627-49a8-ba0e-b1f4014322a5
caps.latest.revision: "12"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: bbff42d43e1bc07dcb163234cab70fcdd9d0582f
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="gettruststore-method-sqlserverdatasource"></a>Método getTrustStore (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getTrustStore()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene la ruta de acceso (incluido el nombre de archivo) en el archivo trustStore del certificado, o null si se establece ningún valor.  
  
## <a name="remarks"></a>Comentarios  
 Si no se establece la propiedad trustStore, el [getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md) método devuelve null.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
