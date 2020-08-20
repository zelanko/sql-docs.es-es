---
description: Archivos DLL de instalación del traductor
title: Archivos dll de instalación de traductor | Microsoft Docs
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
ms.openlocfilehash: 2fe4d514f098773024392666d8f528592d362da4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487398"
---
# <a name="translator-setup-dlls"></a>Archivos DLL de instalación del traductor
> [!NOTE]  
>  A partir de Windows XP y Windows Server 2003, ODBC se incluye en el sistema operativo Windows. Solo debe instalar explícitamente ODBC en versiones anteriores de Windows.  
  
 El archivo DLL de instalación de Translator contiene la función **ConfigTranslator** , que devuelve la opción predeterminada para un traductor. Si es necesario, solicita esta información al usuario. Para obtener una descripción completa de esta función, consulte la referencia de la [API de dll de configuración](../../../odbc/reference/syntax/setup-dll-api-reference.md).  
  
 El programa de instalación de Translator escribe el archivo DLL de configuración de traductor. Puede formar parte de la DLL de traductor o de un archivo DLL independiente.
