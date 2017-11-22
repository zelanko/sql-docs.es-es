---
title: Clase SQLServerParameterMetaData | Documentos de Microsoft
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
ms.assetid: 546290e0-9411-4a2b-aa36-61251e70e9cf
caps.latest.revision: "10"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dd97c5667d774829fb801ad22211d338afde1453
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="sqlserverparametermetadata-class"></a>Clase SQLServerParameterMetaData
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Representa los metadatos para los parámetros de instrucción preparados.  
  
 **Paquete:** com.microsoft.sqlserver.jdbc  
  
 **Extiende:** java.lang.Object  
  
 **Implementa:** java.sql.ParameterMetaData  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public class SQLServerParameterMetaData  
```  
  
## <a name="remarks"></a>Comentarios  
 Para recuperar los metadatos de parámetro, las instrucciones preparadas se ejecutan con SET FMT ONLY. Las instrucciones invocables llaman a sp_sproc_columns para recuperar nombres y metadatos para los parámetros de procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerParameterMetaData](../../../connect/jdbc/reference/sqlserverparametermetadata-members.md)   
 [Referencia de API del controlador JDBC](../../../connect/jdbc/reference/jdbc-driver-api-reference.md)  
  
  
