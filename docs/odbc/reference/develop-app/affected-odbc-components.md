---
title: Componentes ODBC afectados | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], affected components
- application upgrades [ODBC], affected components
- compatibility [ODBC], affected components
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], affected components
ms.assetid: 71fa6ea4-007c-4c2b-b5af-2cec6ea79b58
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: cb58971a193a210f927d1b0a38f2be671b749468
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="affected-odbc-components"></a>Componentes de ODBC afectados
Compatibilidad con versiones anteriores describe cómo las aplicaciones, el Administrador de controladores y los controladores se ven afectados por la introducción de una nueva versión del Administrador de controladores. Esto afecta a las aplicaciones y el controlador cuando una de ellas o ambas permanecen en la versión anterior. Existen, por lo tanto, tres tipos de compatibilidad con versiones anteriores a tener en cuenta, como se muestra en la tabla siguiente.  
  
|Tipo|Versión de DM|Versión de aplicación|Versión del controlador|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidad con versiones anteriores del Administrador de controladores|3*.x*|2.*x*|2.*x*|  
|Compatibilidad con versiones anteriores del controlador [1]|3*.x*|2.*x*|3.*x*|  
|Compatibilidad con versiones anteriores de la aplicación|3.*x*|3.*x*|2.*x*|  
  
 [1] la compatibilidad con versiones anteriores de los controladores se describe principalmente en Apéndice G: controlador directrices para compatibilidad con versiones anteriores.  
  
> [!NOTE]  
>  Una aplicación compatible con los estándares, por ejemplo, una aplicación que se ha escrito según los estándares ISO CLI o de Open Group: se garantiza para trabajar con una aplicación ODBC 3*.x* controlador a través de ODBC 3*.x*El Administrador de controladores. Se supone que las funciones que se utiliza la aplicación está disponible en el controlador. También se supone que se ha compilado la aplicación compatible con los estándares con ODBC 3*.x* archivos de encabezado.
