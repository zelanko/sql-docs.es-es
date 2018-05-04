---
title: Método getClientInfoProperties (SQLServerDatabaseMetaData) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 1568aef4-f4c4-40a0-a1ab-9c106905bd92
caps.latest.revision: 14
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b11f86d2eecc7c3efcc52942f8955ea3381a132c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getclientinfoproperties-method-sqlserverdatabasemetadata"></a>Método getClientInfoProperties (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera una lista de las propiedades de la información de cliente que admite el controlador.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.sql.ResultSet getClientInfoProperties()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un objeto ResultSet.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getClientInfoProperties especificado por el método getClientInfoProperties en la interfaz java.sql.DatabaseMetaData.  
  
> [!NOTE]  
>  Este método devuelve un conjunto de resultados vacío. El controlador permite establecer solamente el **applicationName** y establece la **applicationName** solo en el momento de la conexión. SQL Server no proporciona soporte técnico para actualizar la información de la aplicación cliente una vez se haya establecido la conexión.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
