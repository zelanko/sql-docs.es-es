---
title: Operaciones de la biblioteca de cursores | Documentos de Microsoft
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
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 00469dcf77ae81f5d02765026fe0c1f7194da5d1
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="cursor-library-operations"></a>Operaciones de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad del controlador cursor.  
  
 Si una aplicación que trabaja con una API ODBC 2*.x* controlador realiza llamadas a ODBC 3.* x* biblioteca de cursores, la aplicación puede usar ODBC 3.* x* características que no son compatibles con la API ODBC 2*.x* controlador. Un escritor de la aplicación debe tener cuidado, cómo se utilizan estas características, sin embargo. Uso de ODBC 3. *x* biblioteca de cursores no realiza un ODBC 2*.x* controlador en una aplicación ODBC 3.* x* controlador.
