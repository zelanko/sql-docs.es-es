---
title: Método allProceduresAreCallable (SQLServerDatabaseMetaData) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDatabaseMetaData.allProceduresAreCallable
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 8886137d-455e-497c-afea-4b326eda52f1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: fe10b1c7255b1861de6332cff7fa23344ed12f7a
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80922958"
---
# <a name="allproceduresarecallable-method-sqlserverdatabasemetadata"></a>Método allProceduresAreCallable (SQLServerDatabaseMetaData)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Recupera si el usuario actual tiene los permisos para llamar a todos los procedimientos que devuelve el método [getProcedures](../../../connect/jdbc/reference/getprocedures-method-sqlserverdatabasemetadata.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean allProceduresAreCallable()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si el usuario tiene los permisos para llamar a todos los procedimientos. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Observaciones  
 El método allProceduresAreCallable especifica este método allProceduresAreCallable en la interfaz java.sql.DatabaseMetaData.  
  
## <a name="see-also"></a>Consulte también  
 [Métodos SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-methods.md)   
 [Miembros SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-members.md)   
 [Clase SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md)  
  
  
