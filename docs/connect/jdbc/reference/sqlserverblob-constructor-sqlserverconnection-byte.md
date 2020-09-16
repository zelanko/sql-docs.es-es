---
description: Constructor SQLServerBlob (SQLServerConnection, byte)
title: Constructor SQLServerBlob (SQLServerConnection, byte) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLServerConnection, byte[].SQLServerBlob
apilocation:
- sqljdbc.jar
apitype: Assembly
ms.assetid: 9fe573e3-30db-4828-abab-e9346493e931
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 968c32094196c88ab8eb607e6faa8992de40ed00
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472167"
---
# <a name="sqlserverblob-constructor-sqlserverconnection-byte"></a>Constructor SQLServerBlob (SQLServerConnection, byte)
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Inicializa una nueva instancia de la clase [SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md) cuando se proporcionan un objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) y una matriz **byte**.  
  
> [!NOTE]  
>  Este método se ha dejado de utilizar en la versión 2.0 del controlador JDBC. En su lugar, se usa el método [createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md) de la clase [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
public SQLServerBlob(SQLServerConnection connection,  
                     byte[] data)  
```  
  
#### <a name="parameters"></a>Parámetros  
 *connection*  
  
 Objeto SQLServerConnection.  
  
 *data*  
  
 Matriz **byte**.  
  
## <a name="see-also"></a>Consulte también  
 [Constructores SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-constructors.md)   
 [Miembros SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-members.md)   
 [Clase SQLServerBlob](../../../connect/jdbc/reference/sqlserverblob-class.md)  
  
  
