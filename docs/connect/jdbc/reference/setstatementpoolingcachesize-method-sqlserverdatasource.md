---
title: Método setStatementPoolingCacheSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 02b5bcc9154e99ef6fe9a2c76ceff5032610dd55
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66762373"
---
# <a name="setstatementpoolingcachesize-method-sqlserverdatasource"></a>Método setStatementPoolingCacheSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece el tamaño de la caché de la instrucción preparada para esta conexión. Funciona si disableStatementPooling se establece en false y el valor > 0.
  
## <a name="syntax"></a>Sintaxis  
  
```

public void setStatementPoolingCacheSize(boolean statementPoolingCacheSize);  
```  
  
#### <a name="parameters"></a>Parámetros  
 *statementPoolingCacheSize*  
  
 El nuevo valor de la **valor de statementPoolingCacheSize** propiedad de conexión.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
