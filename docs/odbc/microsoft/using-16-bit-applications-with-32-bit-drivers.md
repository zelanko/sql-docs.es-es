---
title: Usar aplicaciones de 16 bits con controladores de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d4be5d2cacaeca7cf53caa330a126284370ec80f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088192"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits con controladores de 32 bits
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en los nuevos trabajos de desarrollo y planee modificar las aplicaciones que actualmente la utilizan. En su lugar, use el administrador de controladores de 32 bits o 64 bits.  
  
 Puede ejecutar aplicaciones de 16 bits con controladores de 32 bits en el sistema basado en Windows, siempre y cuando el controlador de 32 bits no llame explícitamente a funciones de la API Win32 que crean subprocesos. El subsistema Windows on Windows (WOW) ejecuta las aplicaciones en modo de 16 bits y resuelve las llamadas de 16 bits al sistema operativo. Los archivos dll de ODBC thunk resuelven las llamadas de 16 bits de la aplicación a los controladores de 32 bits. Las aplicaciones de 16 bits usan la API de Windows y los controladores de 32 bits usan la API de Win32.  
  
## <a name="architecture"></a>Architecture  
 En la ilustración siguiente se muestra cómo se comunican las aplicaciones de 16 bits con los controladores de 32 bits. Entre el administrador de controladores de 16 bits y los controladores de 32 bits se encuentran los archivos dll de conversión de tipos genéricos que convierten las llamadas ODBC de 16 bits a llamadas ODBC de 32 bits.  
  
 ![Cómo se comunican 16 aplicaciones de&#45;bits con controladores de 32&#45;bits](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Cada vez que una aplicación de 16 bits interactúa con un controlador de 32 bits, el administrador de controladores de 32 bits siempre devuelve "2,0" como la versión de ODBC compatible con el controlador.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para controladores de 32 bits mediante el administrador de orígenes de datos ODBC. Para abrir el administrador de ODBC en equipos que ejecutan Microsoft® Windows® 2000, abra el panel de control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. En los equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC de 32 bits** o simplemente **ODBC**.  
  
 En la ilustración siguiente se muestra cómo una aplicación de 16 bits llama a un archivo DLL de instalación del controlador de 32 bits. Entre el archivo DLL del instalador de 16 bits y el archivo DLL de instalación del controlador de 32 bits se encuentra un archivo DLL de thunk genérico que convierte las llamadas DLL del instalador de 16 bits a llamadas DLL del instalador de 32 bits.  
  
 ![Cómo una aplicación de 16&#45;bits llama a un archivo DLL de instalación del controlador de 32&#45;bits](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 En Windows en Windows (thunk de 16 bits a 32 bits), una DLL de thunk adicional denominada Ds32gt. dll convierte los valores de argumento de 16 bits que se pasan a través de un archivo DLL de instalación de 32 bits de nuevo a 16 bits.  
  
## <a name="components"></a>Componentes  
 El componente ODBC del SDK de MDAC 2,8 SP1 incluye los siguientes archivos para ejecutar aplicaciones de 16 bits con controladores de 32 bits. Estos componentes se encuentran en el directorio \Redist  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc16gt. dll|DLL de conversión genérica ODBC de 16 bits|  
|Odbc32gt. dll|DLL de conversión genérica ODBC de 32 bits|  
|Odbccp32. dll|DLL del instalador de 32 bits|  
|Odbcad32. exe|Programa de administrador de 32 bits|  
|Odbcinst. hlp|Archivo de ayuda del instalador|  
|Ds16gt. dll|DLL de conversión genérica de instalación del controlador de 16 bits|  
|Ctl3d32. dll|Biblioteca de estilos de ventanas tridimensionales de 32 bits|  
  
 Además, los siguientes archivos junto con el administrador de controladores ODBC 2,10 de 16 bits, que no forman parte de ODBC 3,51, son necesarios para y deben instalarse con la aplicación de 16 bits.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|ODBC. dll|Administrador de controladores de 16 bits|  
|Odbcinst. dll|DLL del instalador de 16 bits|  
|Odbcadm. exe|Programa de administrador de ODBC de 16 bits|
