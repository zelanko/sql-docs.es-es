---
description: Tipo de cursor y combinaciones de simultaneidad
title: Tipos de cursor y combinaciones de simultaneidad | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], concurrency options
- cursors [ODBC], ODBC driver for Oracle
- concurrency options [ODBC]
- ODBC driver for Oracle [ODBC], cursor options
ms.assetid: db63d610-f86f-4029-9d66-fed616c8a818
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae82825f7b5c6f670e111b859ee02ab4ab875626
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88412912"
---
# <a name="cursor-type-and-concurrency-combinations"></a>Tipo de cursor y combinaciones de simultaneidad
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Los tipos de cursor controlan la funcionalidad del cursor que se proporciona al usuario. Las opciones de simultaneidad controlan la capacidad de actualización y el comportamiento de bloqueo de un conjunto de resultados.  
  
|Tipo de cursor|Simultaneidad (valores permitidos)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_READ_ONLY SQL_CONCUR_LOCK<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1]</sup> vea las [limitaciones del uso de cursores controlados por conjunto de claves](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2]</sup> SQL_CONCUR_LOCK solo se admite cuando la opción de conexión SQL_AUTOCOMMIT está establecida en SQL_AUTOCOMMIT_OFF.  
  
## <a name="see-also"></a>Consulte también  
 [Opciones de conexión](../../odbc/microsoft/connect-options.md)
