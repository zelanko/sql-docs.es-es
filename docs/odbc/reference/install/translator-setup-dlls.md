---
title: DLL de configuración del traductor ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator setup DLL [ODBC]
ms.assetid: b3ca79e9-01b9-4541-81de-bbbad24ca736
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 28c354fddb36b9e035361fa4ba03fbde34b7d399
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296055"
---
# <a name="translator-setup-dlls"></a>Archivos DLL de instalación del traductor
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar ODBC explícitamente en versiones anteriores de Windows.  
  
 El archivo DLL de instalación del traductor contiene la función **ConfigTranslator,** que devuelve la opción predeterminada para un traductor. Si es necesario, solicita al usuario esta información. Para obtener una descripción completa de esta función, consulte Referencia de la [API de DLL](../../../odbc/reference/syntax/setup-dll-api-reference.md)de instalación .  
  
 El archivo DLL de instalación del traductor está escrito por el desarrollador del traductor. Puede ser parte de la DLL del traductor o un archivo DLL independiente.
