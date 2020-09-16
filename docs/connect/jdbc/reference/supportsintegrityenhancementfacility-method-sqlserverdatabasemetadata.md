---
description: Método supportsIntegrityEnhancementFacility (SQLServerDatabaseMetaData)
title: Método supportsIntegrityEnhancementFacility | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsIntegrityEnhancementFacility
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: edee084b-9a8c-4167-9e13-66fc3ed1ecaa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4c3826871bd68bc7ba99dd2230d545ecdfcf4975
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88450393"
---
# <a name="supportsintegrityenhancementfacility-method-sqlserverdatabasemetadata"></a>Método supportsIntegrityEnhancementFacility (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite SQL Integrity Enhancement Facility.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsIntegrityEnhancementFacility()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsIntegrityEnhancementFacility especifica este método supportsIntegrityEnhancementFacility en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
