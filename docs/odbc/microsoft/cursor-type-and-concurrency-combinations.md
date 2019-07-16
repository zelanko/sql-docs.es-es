---
title: Tipo de cursor y combinaciones de simultaneidad | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 2a29fc2d02cb46dda44fa22b2344cbab475443f2
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68096530"
---
# <a name="cursor-type-and-concurrency-combinations"></a>Tipo de cursor y combinaciones de simultaneidad
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Tipos de cursor controlan la funcionalidad del cursor proporcionada al usuario. Opciones de simultaneidad controlan la posibilidad de actualización y el comportamiento de bloqueo de un conjunto de resultados.  
  
|Tipo de cursor|Simultaneidad (los valores permitidos)|  
|-----------------|------------------------------------|  
|SQL_CURSOR_FORWARD_ONLY|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_STATIC|SQL_CONCUR_READ_ONLY|  
|SQL_CURSOR_KEYSET_DRIVEN<sup>[1]</sup>|SQL_CONCUR_LOCK SQL_CONCUR_READ_ONLY<sup>[2]</sup> SQL_CONCUR_VALUES|  
  
 <sup>[1] </sup> Vea [limitaciones del uso de los cursores dinámicos](../../odbc/microsoft/limitations-of-using-keyset-driven-cursors.md).  
  
 <sup>[2] </sup> SQL_CONCUR_LOCK solo se admite cuando la opción de conexión SQL_AUTOCOMMIT está establecida en SQL_AUTOCOMMIT_OFF.  
  
## <a name="see-also"></a>Vea también  
 [Opciones de conexión](../../odbc/microsoft/connect-options.md)
