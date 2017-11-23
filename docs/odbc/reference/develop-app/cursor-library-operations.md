---
title: Operaciones de la biblioteca de cursores | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 25c26cfd81d4ad494406a0559b98c8d6e85a7ded
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/20/2017
---
# <a name="cursor-library-operations"></a>Operaciones de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Si una aplicación que trabaja con una API ODBC 2*.x* controlador realiza llamadas a ODBC 3. *x* biblioteca de cursores, la aplicación puede usar ODBC 3. *x* características que no son compatibles con la API ODBC 2*.x* controlador. Un escritor de la aplicación debe tener cuidado, cómo se utilizan estas características, sin embargo. Uso de ODBC 3. *x* biblioteca de cursores no realiza un ODBC 2*.x* controlador en una aplicación ODBC 3. *x* controlador.
