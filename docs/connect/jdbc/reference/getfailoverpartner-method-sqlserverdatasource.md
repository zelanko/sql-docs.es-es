---
title: Método getFailoverPartner (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLServerDataSource.getFailoverPartner
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 885f927f-9c48-42e0-a7fb-fd936d2b8130
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7633fd2fe5137ee7c04bf10ebe0c40b367c35f64
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getfailoverpartner-method-sqlserverdatasource"></a>Método getFailoverPartner (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el nombre del servidor de conmutación por error que se utiliza en una configuración de creación de reflejo de la base de datos.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public string getFailoverPartner()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 A **cadena** que contiene el nombre del asociado de conmutación por error, o null si no se establece ninguno.  
  
## <a name="remarks"></a>Comentarios  
 El valor devuelto por este método refleja utilizando del espacio de nombre de asociado de conmutación por error el [setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md) método.  
  
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
