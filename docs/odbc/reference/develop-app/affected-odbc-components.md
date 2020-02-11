---
title: Componentes ODBC afectados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 08997f610b00f22d436a5c91d34beb2a8fc2cc1d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944854"
---
# <a name="affected-odbc-components"></a>Componentes de ODBC afectados
La compatibilidad con versiones anteriores describe el modo en que las aplicaciones, el administrador de controladores y los controladores se ven afectados por la introducción de una nueva versión del administrador de controladores. Esto afecta a las aplicaciones y al controlador cuando uno o ambos permanecen en la versión anterior. Por lo tanto, hay tres tipos de compatibilidad con versiones anteriores que se deben tener en cuenta, como se muestra en la tabla siguiente.  
  
|Tipo|Versión de DM|Versión de la aplicación|Versión del controlador|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidad con versiones anteriores del administrador de controladores|*3.x*|*2.x*|*2.x*|  
|Compatibilidad con versiones anteriores del controlador [1]|*3.x*|*2.x*|*3.x*|  
|Compatibilidad con versiones anteriores de la aplicación|*3.x*|*3.x*|*2.x*|  
  
 [1] la compatibilidad con versiones anteriores de los controladores se describe principalmente en el Apéndice G: instrucciones de controlador para la compatibilidad con versiones anteriores.  
  
> [!NOTE]
>  Una aplicación compatible con los estándares (por ejemplo, una aplicación que se ha escrito de acuerdo con los estándares Open Group o ISO CLI) está garantizada para que funcione con un controlador ODBC *3. x* a través del administrador de controladores ODBC *3. x* . Se supone que la funcionalidad que está usando la aplicación está disponible en el controlador. También se supone que la aplicación compatible con los estándares se ha compilado con los archivos de encabezado ODBC *3. x* .
