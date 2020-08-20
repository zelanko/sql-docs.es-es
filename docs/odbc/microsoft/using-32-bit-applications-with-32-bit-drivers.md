---
description: Uso de las aplicaciones de 32 bits con controladores de 32 bits
title: Usar aplicaciones de 32 bits con controladores de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 69005071c83047471e76f38160265bc35cdccd4b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471369"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 32 bits con controladores de 32 bits
Puede ejecutar aplicaciones de 32 bits con controladores de 32 bits. Las aplicaciones de 32 bits y los controladores de 32 bits usan la API de® Win32.  
  
## <a name="architecture"></a>Architecture  
 En la ilustración siguiente se muestra cómo se comunican las aplicaciones de 32 bits con los controladores de 32 bits. La aplicación llama al administrador de controladores de 32 bits, que a su vez llama a los controladores de 32 bits.  
  
 ![Cómo se comunican las aplicaciones de&#45;bits de 32 con los controladores de 32&#45;bits](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  No use el archivo DLL del instalador de thunk de 32 bits en WindowsNT/windows2000. Aunque tiene el mismo nombre de archivo que el archivo DLL del instalador de 32 bits, es un archivo DLL diferente.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para controladores de 32 bits mediante el administrador de orígenes de datos ODBC. Para abrir el administrador de ODBC en equipos que ejecutan Windows 2000, abra el panel de control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. En los equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC de 32 bits** o simplemente **ODBC**.  
  
## <a name="components"></a>Componentes  
 El componente ODBC incluye los siguientes archivos para ejecutar aplicaciones de 32 bits con controladores de 32 bits. Estos componentes se encuentran en el directorio \Redist  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc32.dll|Administrador de controladores de 32 bits|  
|Odbccp32.dll|DLL del instalador de 32 bits|  
|Odbcad32.exe|Programa de administrador de ODBC de 32 bits|  
|Odbcinst. hlp|Archivo de ayuda del instalador|  
|Msvcrt40.dll|Biblioteca en tiempo de ejecución de C|
