---
title: Método supportsCorrelatedSubqueries (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.supportsCorrelatedSubqueries
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 85bb1bcc-31ae-4f6b-a103-699724bbb0aa
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89ab9bc4d60605c17422ebbfe2192d05ab72d0c4
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80928106"
---
# <a name="supportscorrelatedsubqueries-method-sqlserverdatabasemetadata"></a>Método supportsCorrelatedSubqueries (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si esta base de datos admite subconsultas correlacionadas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean supportsCorrelatedSubqueries()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 **true** si es compatible. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método supportsCorelatedSubqueries especifica este método supportsCorelatedSubqueries en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
