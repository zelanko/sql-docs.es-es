---
title: getStatementPoolingCacheSize (método) (SQLServerDataSource) | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ''
caps.latest.revision: 1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2ca786e4c902435b1d474c05f8947e3bc62424a5
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32837699"
---
# <a name="getstatementpoolingcachesize-method-sqlserverdatasource"></a>getStatementPoolingCacheSize (método) (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de **statementPoolingCacheSize** propiedad de conexión. Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. '0' significa que no está habilitada la memoria caché.
  
## <a name="syntax"></a>Sintaxis  
  
```
public boolean getStatementPoolingCacheSize();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El **int** valor de la **statementPoolingCacheSize** propiedad de conexión.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Comentarios  
 Este método está disponible desde la versión del controlador JDBC 6.4 y hacia delante.
 
## <a name="see-also"></a>Vea también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
