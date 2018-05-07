---
title: Método getMoreResults (int) | Documentos de Microsoft
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
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 75609ec8f24674dd7ff9d1a6724cbc458be47f84
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="getmoreresults-method-int"></a>Método getMoreResults (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se desplaza al próximo resultado de esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto y se ocupa de cualquier resultado abierto actualmente conjunto de objetos según las instrucciones que determina el modo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *Modo*  
  
 Un **int** que indica cómo administrar objetos de conjunto de resultados abiertos actualmente. Debe ser una de las constantes siguientes:  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (no admitido por el controlador JDBC)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Valor devuelto  
 **True** si el resultado devuelto es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Comentarios  
 Este método getMoreResults especificado por el método getMoreResults en la interfaz java.sql.Statement.  
  
 Si se llama al método getMoreResults antes de que se recuperan los resultados, se comporta según lo especificado por el *modo* argumento y se desplaza hasta el siguiente resultado.  
  
> [!NOTE]  
>  El controlador JDBC no admite el uso de la constante KEEP_CURRENT_RESULT. Si se utiliza, se producirá una excepción.  
  
## <a name="see-also"></a>Vea también  
 [Método getMoreResults &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
