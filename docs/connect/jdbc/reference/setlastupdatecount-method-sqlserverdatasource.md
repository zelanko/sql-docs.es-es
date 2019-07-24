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
ms.openlocfilehash: fd9776dd60e82067b0d048e2f385b2bc685b79ea
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67974119"
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
  
 **true** si lastUpdateCount está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Notas  
 Si la propiedad lastUpdateCount está establecida en **true**, [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] solo devolverá el último recuento de actualizaciones a partir de una instrucción SQL que se haya pasado al servidor. Si la propiedad lastUpdateCount está establecida en **false**, el controlador devolverá todos los recuentos de actualizaciones, incluso los que se hayan devuelto por desencadenadores activados. Si no se establece la propiedad lastUpdateCount, el método [getLastUpdateCount ](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)devuelve el valor predeterminado **true**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
