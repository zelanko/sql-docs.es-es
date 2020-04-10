---
title: Método getStatementPoolingCacheSize (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2018
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
ms.assetid: ''
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2ef133c2c661cd9c4778d6ca9b3efec8e51d5a5d
ms.sourcegitcommit: fe5c45a492e19a320a1a36b037704bf132dffd51
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2020
ms.locfileid: "80926228"
---
# <a name="getstatementpoolingcachesize-method-sqlserverdatasource"></a>Método getStatementPoolingCacheSize (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve el valor de la propiedad de conexión **statementPoolingCacheSize**. Devuelve el tamaño de la caché de instrucciones preparadas para esta conexión. "0" significa que el almacenamiento en caché no está habilitado.
  
## <a name="syntax"></a>Sintaxis  
  
```
public boolean getStatementPoolingCacheSize();  
```  
  
## <a name="return-value"></a>Valor devuelto  
 El valor de **int** de la propiedad de conexión **statementPoolingCacheSize**.  

## <a name="exceptions"></a>Excepciones  
 [SQLServerException](../../../connect/jdbc/reference/sqlserverexception-class.md)  
 
## <a name="remarks"></a>Observaciones  
 Este método está disponible en la versión 6.4 y posteriores del controlador JDBC.
 
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
