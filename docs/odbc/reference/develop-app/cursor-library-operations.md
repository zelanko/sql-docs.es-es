---
title: Operaciones de la biblioteca de cursores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], backward compatibility
- compatibility [ODBC], cursor library
- upgrading applications [ODBC], cursor library
- application upgrades [ODBC], cursor library
- backward compatibility [ODBC], cursor library
- cursor library [ODBC], backward compatibility
ms.assetid: 04d514b1-dc4d-4b84-bf35-60f4657ef1f6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 32e3fcaf9c83c2613a1dc2df499f11c7df2570ad
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63042141"
---
# <a name="cursor-library-operations"></a>Operaciones de la biblioteca de cursores
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Microsoft recomienda usar la funcionalidad de cursor del controlador.  
  
 Si una aplicación trabajar con un ODBC 2 *.x* controlador realiza llamadas a la ODBC 3. *x* biblioteca de cursores, la aplicación podría ser capaz de utilizar ODBC 3. *x* características que no son compatibles con la API ODBC 2 *.x* controlador. Un escritor de la aplicación debe tener cuidado, cómo se utilizan estas características, sin embargo. Uso de ODBC 3. *x* biblioteca de cursores no realiza un ODBC 2 *.x* controlador en una aplicación ODBC 3. *x* controlador.
