---
title: Método getDisableStatementPooling (SQLServerDataSource) | Microsoft Docs
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
ms.openlocfilehash: 607d729726c421030f4f77247b4e0090c900744c
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66776830"
---
# <a name="getdisablestatementpooling-method-sqlserverdatasource"></a>Método getDisableStatementPooling (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de **disableStatementPooling** propiedad de conexión. Esta configuración controla si se habilita la agrupación de la instrucción o no para esta conexión.

  
## <a name="syntax"></a>Sintaxis  
  
```
public boolean getDisableStatementPooling();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Un **booleano** que contiene el valor de **disableStatementPooling** propiedad de conexión.
  
## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Notas  
 Este método está disponible desde la versión del controlador JDBC 6.4 y en marcha.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
