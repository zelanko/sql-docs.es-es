---
title: Método getMoreResults (int) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerStatement.getMoreResults (int)
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 6419e5a8-8b3a-4d5b-8226-95865c52c723
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a7d4fe32d7d1ac4be9a20923fc4d230ac64d1c8d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47667813"
---
# <a name="getmoreresults-method-int"></a>Método getMoreResults (int)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Se desplaza al resultado siguiente de este objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) y se ocupa de los objetos del conjunto de resultados abiertos en esos momentos de acuerdo a las instrucciones que determina el modo especificado.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public final boolean getMoreResults(int mode)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *mode*  
  
 Un valor **int** que indica cómo administrar los objetos del conjunto de resultados abiertos en esos momentos. Es preciso que sea una de las constantes siguientes:  
  
 CLOSE_CURRENT_RESULT  
  
 KEEP_CURRENT_RESULT (no admitido por el controlador JDBC)  
  
 CLOSE_ALL_RESULTS  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si el resultado devuelto es un conjunto de resultados. De lo contrario, se devuelve el valor **False**.  
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
  
## <a name="remarks"></a>Notas  
 Este método getMoreResults especificado por el método getMoreResults en la interfaz java.sql.Statement.  
  
 Si se llama al método getMoreResults antes de que se recuperen los resultados, se comporta tal como especificó el argumento *mode* y avanza al resultado siguiente.  
  
> [!NOTE]  
>  El controlador JDBC no admite el uso de la constante KEEP_CURRENT_RESULT. Si se utiliza, se producirá una excepción.  
  
## <a name="see-also"></a>Ver también  
 [Método getMoreResults &#40;SQLServerStatement&#41;](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)   
 [Miembros SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-members.md)   
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
