---
title: Procesamiento de lotes de instrucciones SQL | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], batches
- ODBC cursor library [ODBC], statement processing
- cursor library [ODBC], batches
- SQL statements [ODBC], cursor library
- cursor library [ODBC], statement processing
- SQL statements [ODBC], batches
- batches [ODBC], processing batches of SQL statements
ms.assetid: 04b93ef9-11de-47a3-8bd8-ba963c42f182
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: a1513b2c9576d994ea7eb505c4928fd609e9498c
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="processing-batches-of-sql-statements"></a>Procesamiento de lotes de instrucciones SQL
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 La biblioteca de cursores no admite lotes de instrucciones SQL, incluidas las instrucciones de SQL para que el atributo de instrucción de SQL_ATTR_PARAMSET_SIZE es mayor que 1. Si una aplicación envía un lote de instrucciones SQL para la biblioteca de cursores, los resultados son indefinidos.

