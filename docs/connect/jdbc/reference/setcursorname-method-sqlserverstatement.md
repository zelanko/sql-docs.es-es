---
title: "Método setCursorName (SQLServerStatement) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLServerStatement.setCursorName
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 3f3ec4f2-103a-4e16-9206-c5bd8639f946
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 501440dec2f47c4f3f272ebde7f6cbd01642e377
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setcursorname-method-sqlserverstatement"></a>Método setCursorName (SQLServerStatement)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el nombre de cursor de SQL para la cadena determinada, el cual utilizarán métodos ulteriores.  
  
> [!NOTE]  
>  Este método no es compatible actualmente con la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]. Si se llama a este método no habrá resultado alguno.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final void setCursorName(java.lang.String name)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Nombre*  
  
 A **cadena** que contiene el nombre del cursor.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método setCursorName especificado por el método setCursorName en la interfaz java.sql.Statement.  
  
## <a name="see-also"></a>Vea también  
 [Miembros de SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
