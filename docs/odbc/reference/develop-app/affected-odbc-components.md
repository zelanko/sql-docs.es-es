---
title: Los componentes ODBC afectados | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 72e004e6fd41ee74643fc05ec9020e6ac1933e09
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208574"
---
# <a name="affected-odbc-components"></a>Componentes de ODBC afectados
Compatibilidad con versiones anteriores, describe cómo las aplicaciones, el Administrador de controladores y los controladores se ven afectados por la introducción de una nueva versión del Administrador de controladores. Esto afecta a las aplicaciones y controladores cuando cualquiera de ellas o ambas permanecen en la versión anterior. Hay, por lo tanto, tres tipos de compatibilidad con versiones anteriores que deben considerarse, como se muestra en la tabla siguiente.  
  
|Tipo|Versión de DM|Versión de aplicación|Versión del controlador|  
|----------|-------------------|----------------------------|-----------------------|  
|Compatibilidad con versiones anteriores del Administrador de controladores|3 *.x*|2.*x*|2.*x*|  
|Compatibilidad con versiones anteriores del controlador [1]|3 *.x*|2.*x*|3.*x*|  
|Compatibilidad con versiones anteriores de la aplicación|3.*x*|3.*x*|2.*x*|  
  
 [1] la compatibilidad con versiones anteriores de los controladores se trata principalmente en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
> [!NOTE]
>  Una aplicación compatible con los estándares: por ejemplo, una aplicación que se ha escrito con arreglo a los estándares ISO CLI o de Open Group: se garantiza para trabajar con una aplicación ODBC 3 *.x* controlador mediante el ODBC 3 *.x*Administrador de controladores. Se supone que las funciones que se utiliza la aplicación está disponible en el controlador. También se supone que se ha compilado la aplicación conforme a los estándares con ODBC 3 *.x* archivos de encabezado.
