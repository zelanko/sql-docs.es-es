---
title: "Método setEscapeProcessing (SQLServerStatement) | Documentos de Microsoft"
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
apiname: SQLServerStatement.setEscapeProcessing
apilocation: sqljdbc.jar
apitype: Assembly
ms.assetid: 6ac0682e-e04c-4fdb-893b-92408d42051e
caps.latest.revision: "11"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b3c59b96934734b23512039a5748df17c92a6ef8
ms.sourcegitcommit: 2713f8e7b504101f9298a0706bacd84bf2eaa174
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/18/2017
---
# <a name="setescapeprocessing-method-sqlserverstatement"></a>Método setEscapeProcessing (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el modo de procesamiento de escape.  
  
> [!NOTE]  
>  El proceso de escape [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] siempre está habilitada. Si este método se establece en "false", no tendrá efecto alguno.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setEscapeProcessing(boolean enable)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *habilitar*  
  
 **True** para habilitar el procesamiento de escape. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setEscapeProcessing especificado por el método setEscapeProcessing en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
