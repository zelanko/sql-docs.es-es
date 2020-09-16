---
description: Método getLastUpdateCount (SQLServerDataSource)
title: Método getLastUpdateCount (SQLServerDataSource) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerDataSource.getLastUpdateCount
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 4c4fbb24-0b02-42da-928c-a903bb591cc7
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 44b5b9c19b07479aaeae6eb400d3212accd3e5fa
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88435777"
---
# <a name="getlastupdatecount-method-sqlserverdatasource"></a>Método getLastUpdateCount (SQLServerDataSource)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Devuelve un valor **boolean** que indica si la propiedad lastUpdateCount está habilitada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public boolean getLastUpdateCount()  
```  
  
## <a name="return-value"></a>Valor devuelto  
 Es **true** si lastUpdateCount está habilitado. De lo contrario, se devuelve el valor **False**.  
  
## <a name="remarks"></a>Observaciones  
 Si la propiedad lastUpdateCount está establecida en **true**, el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] solo devolverá el último recuento de actualizaciones a partir de una instrucción SQL que se haya pasado al servidor. Si la propiedad lastUpdateCount está establecida en **false**, el controlador devolverá todos los recuentos de actualizaciones, incluso los que se hayan devuelto por desencadenadores activados. Si no se establece la propiedad lastUpdateCount, el método getLastUpdateCount devuelve el valor predeterminado **true**.  
  
## <a name="see-also"></a>Consulte también  
 [Miembros SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-members.md)   
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
