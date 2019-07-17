---
title: Archivos DLL de instalación de traductor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: b6c99dffc94f2675efdbbc3d5c1d142a5ae9b7e5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093838"
---
# <a name="translator-setup-dlls"></a>Archivos DLL de instalación del traductor
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El programa de instalación de traductor DLL contiene la **ConfigTranslator** función, que devuelve la opción predeterminada para un traductor. Si es necesario, pide al usuario esta información. Para obtener una descripción completa de esta función, vea [referencia de API de DLL de instalación](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 El programa de instalación del traductor DLL está escrita por el programador de traductor. Puede ser parte del traductor de DLL o un archivo DLL independiente.
