---
title: Método setLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.setLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 5487631a-1107-4169-84ca-b77fd09bea66
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: edc0b28c132e5422c12ae340e35c1464ee48fa73
ms.sourcegitcommit: ad2e98972a0e739c0fd2038ef4a030265f0ee788
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2019
ms.locfileid: "66799250"
---
# <a name="setlastupdatecount-method-sqlserverdatasource"></a>Método setLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Establece un valor **booleano** que indica si la propiedad lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public void setLastUpdateCount(boolean lastUpdateCount)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *lastUpdateCount*  
  
 **True** si lastUpdateCount está habilitada. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad lastUpdateCount está establecida en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] solo devolverá el último recuento de actualizaciones a partir de una instrucción SQL que se haya pasado al servidor. Si la propiedad lastUpdateCount está establecida en **false**, el controlador devolverá todos los recuentos de actualizaciones, incluso los que se hayan devuelto por desencadenadores activados. Si no se establece la propiedad lastUpdateCount, el método [getLastUpdateCount ](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)devuelve el valor predeterminado **true**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
