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
manager: craigg
ms.openlocfilehash: 20453b792ed00b388977fefe3064fd8dfca86147
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63273289"
---
# <a name="translator-setup-dlls"></a>Archivos DLL de instalación del traductor
> [!NOTE]  
>  Desde Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. ODBC explícitamente sólo debe instalar en versiones anteriores de Windows.  
  
 El programa de instalación de traductor DLL contiene la **ConfigTranslator** función, que devuelve la opción predeterminada para un traductor. Si es necesario, pide al usuario esta información. Para obtener una descripción completa de esta función, vea [referencia de API de DLL de instalación](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 El programa de instalación del traductor DLL está escrita por el programador de traductor. Puede ser parte del traductor de DLL o un archivo DLL independiente.
