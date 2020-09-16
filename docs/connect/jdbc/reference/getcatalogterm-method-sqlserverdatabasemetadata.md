---
description: Método getCatalogTerm (SQLServerDatabaseMetaData)
title: Método getCatalogTerm (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.getCatalogTerm
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 0aa5d372-16aa-4790-a8f6-f8b742798f8f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: a9f0625997adaea84808bd8ace89173ce5798f8d
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88436877"
---
# <a name="getcatalogterm-method-sqlserverdatabasemetadata"></a>Método getCatalogTerm (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera el término preferido del proveedor de la base de datos para "catálogo".  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public java.lang.String getCatalogTerm()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Objeto **String** que contiene el término de catálogo.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método getCatalogTerm especifica este método getCatalogTerm en la interfaz java.sql.DatabaseMetaData.  
  
 Cuando el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] se usa con una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], este método devuelve el término "base de datos".  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
