---
title: bcp_batch | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
api_name:
- bcp_batch
api_location:
- sqlncli11.dll
topic_type:
- apiref
helpviewer_keywords:
- bcp_batch function
ms.assetid: 0bda489e-86bc-4a7e-80f6-96047e03f281
author: rothja
ms.author: jroth
ms.openlocfilehash: a028ed31ff2f4936d5d7bd45ba7809467939718b
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85019898"
---
# <a name="bcp_batch"></a>bcp_batch
  Confirma todas las filas previamente copiadas de forma masiva desde variables de programa y enviadas a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a través de [bcp_sendrow](bcp-sendrow.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
DBINT bcp_batch (HDBC  
hdbc  
);  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *hdbc*  
 Es el identificador de la conexión ODBC habilitada para la copia masiva.  
  
## <a name="returns"></a>Devoluciones  
 El número de filas guardado después de la última llamada a **bcp_batch**, o-1 en caso de error.  
  
## <a name="remarks"></a>Comentarios  
 Los lotes de copia masiva definen las transacciones. Cuando una aplicación usa [bcp_bind](bcp-bind.md) y **bcp_sendrow** para copiar filas de forma masiva de variables de programa a las tablas de SQL Server, las filas solo se confirman cuando el programa llama a **bcp_batch** o a [bcp_done](bcp-done.md).  
  
 Puede llamar a **bcp_batch** una vez cada *n* filas o cuando se produzcan períodos de inactividad en la entrada de datos (como en una aplicación de telemetría). Si una aplicación no llama a **bcp_batch** , las filas copiadas de forma masiva solo se confirmarán cuando se llame a **bcp_done** .  
  
## <a name="see-also"></a>Consulte también  
 [Bulk Copy Functions](sql-server-driver-extensions-bulk-copy-functions.md)  
  
  
