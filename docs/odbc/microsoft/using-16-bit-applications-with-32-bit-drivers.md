---
title: Uso de aplicaciones de 16 bits con controladores de 32 bits | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 3ebd6f25758f73e75fd96abb734bc7b0347d5ee0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209972"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits con controladores de 32 bits
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite usar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Use el Administrador de controladores de 32 bits o 64 bits en su lugar.  
  
 Puede ejecutar aplicaciones de 16 bits con controladores de 32 bits en un sistema basado en Windows, siempre que el controlador de 32 bits no llamar explícitamente a funciones API de Win32 que crean subprocesos. El Windows en el subsistema de Windows (WOW) ejecuta las aplicaciones en modo de 16 bits y resuelve las llamadas de 16 bits en el sistema operativo. ODBC thunk dll resolve llamadas de 16 bits de la aplicación a los controladores de 32 bits. Las aplicaciones de 16 bits utilizan la API de Windows y controladores de 32 bits utilizan la API Win32.  
  
## <a name="architecture"></a>Architecture  
 La siguiente ilustración muestra las aplicaciones de 16 bits cómo comunicarse con los controladores de 32 bits. Entre el Administrador de controladores de 16 bits y los controladores de 32 bits que son genéricos thunk archivos DLL que conversión las llamadas a ODBC de 16 bits a las llamadas ODBC de 32 bits.  
  
 ![Cómo 16&#45;las aplicaciones de bits se comunican con 32&#45;bit controladores](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Cada vez que una aplicación de 16 bits interactúa con un controlador de 32 bits, el Administrador de controladores de 32 bits siempre devuelve "2.0" como la versión de ODBC compatibles con el controlador.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para los controladores de 32 bits mediante el Administrador de orígenes de datos ODBC. Para abrir el Administrador de ODBC en equipos que ejecutan Microsoft® Windows® 2000, abra el Panel de Control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)** . En equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC 32-bit** o simplemente **ODBC**.  
  
 La siguiente ilustración muestra cómo una aplicación de 16 bits llama a un archivo DLL de configuración del controlador de 32 bits. Entre la DLL de instalador de 16 bits y el controlador de 32 bits DLL de instalación es una DLL de thunk genérica que convierte las llamadas DLL de instalador de 16 bits a las llamadas DLL de instalador de 32 bits.  
  
 ![Cómo un 16&#45;bits aplicación llama a un 32&#45;DLL de instalación de controlador de bits](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 En Windows en Windows (thunk de 16 bits a 32 bits), una DLL thunk adicional denominada convierte Ds32gt.dll valores de argumento de 16 bits que se pasan a través de un programa de instalación de 32 bits DLL apoyar a 16 bits.  
  
## <a name="components"></a>Componentes  
 El componente de ODBC de los SDK de MDAC 2.8 SP1 incluye los siguientes archivos para ejecutar aplicaciones de 16 bits con controladores de 32 bits. Estos componentes están en el directorio \Redist.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL thunk de 16 bits ODBC genérico|  
|Odbc32gt.dll|DLL de 32 bits ODBC genérico thunk|  
|Odbccp32.dll|DLL de instalador de 32 bits|  
|Odbcad32.exe|programa del Administrador de 32 bits|  
|Odbcinst.hlp|Archivo de Ayuda del instalador|  
|Ds16gt.dll|instalación del controlador de 16 bits genérica thunk DLL|  
|Ctl3d32.dll|biblioteca de estilo de ventana tridimensional de 32 bits|  
  
 Además, los siguientes archivos junto con el Administrador de controlador de ODBC 2.10 de 16 bits, que no forman parte de ODBC 3.51, se requieren y deben instalarse con la aplicación de 16 bits.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc.dll|Administrador de controladores de 16 bits|  
|Odbcinst.dll|DLL de instalador de 16 bits|  
|Odbcadm.exe|programa de administrador de ODBC de 16 bits|
