---
title: Uso de aplicaciones de 16 bits con controladores de 32 bits Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c919ed8c3f3791720d67ebdcbf5cfbdbea2a0455
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307636"
---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits con controladores de 32 bits
> [!IMPORTANT]  
>  Esta característica se eliminará en una versión futura de Windows. Evite usar esta característica en el nuevo trabajo de desarrollo y planee modificar las aplicaciones que actualmente utilizan esta característica. Utilice el administrador de controladores de 32 bits o 64 bits en su lugar.  
  
 Puede ejecutar aplicaciones de 16 bits con controladores de 32 bits en el sistema basado en Windows, siempre que el controlador de 32 bits no llame explícitamente a las funciones de la API de Win32 que crean subprocesos. El subsistema Windows en Windows (WOW) ejecuta las aplicaciones en modo de 16 bits y resuelve las llamadas de 16 bits al sistema operativo. Los archivos DLL de thunking ODBC resuelven llamadas de 16 bits desde la aplicación a controladores de 32 bits. Las aplicaciones de 16 bits usan la API de Windows y los controladores de 32 bits usan la API de Win32.  
  
## <a name="architecture"></a>Architecture  
 En la siguiente ilustración se muestra cómo se comunican las aplicaciones de 16 bits con los controladores de 32 bits. Entre el Administrador de controladores de 16 bits y los controladores de 32 bits son archivos DLL de thunking genéricos que convierten las llamadas ODBC de 16 bits a llamadas ODBC de 32 bits.  
  
 ![Cómo se comunican las aplicaciones de 16&#45;bits con controladores de 32&#45;bits](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Cada vez que una aplicación de 16 bits interactúa con un controlador de 32 bits, el Administrador de controladores de 32 bits siempre devuelve "2.0" como la versión de ODBC compatible con el controlador.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para controladores de 32 bits mediante el Administrador de orígenes de datos ODBC. Para abrir el Administrador ODBC en equipos que ejecutan Microsoft® Windows® 2000, abra el Panel de control de Windows, haga doble clic en **Herramientas administrativas**y, a continuación, haga doble clic en Orígenes de datos **(ODBC)**. En equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina ODBC de **32 bits** o simplemente **ODBC**.  
  
 En la siguiente ilustración se muestra cómo una aplicación de 16 bits llama a un archivo DLL de instalación de controlador de 32 bits. Entre el archivo DLL del instalador de 16 bits y el archivo DLL de instalación del controlador de 32 bits es un archivo DLL genérico que convierte las llamadas DLL del instalador de 16 bits en llamadas DLL del instalador de 32 bits.  
  
 ![Cómo una aplicación de 16&#45;bits llama a un archivo DLL de configuración de controlador de 32&#45;bits](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 En Windows en Windows (thunking de 16 bits a 32 bits), un archivo DLL thunking adicional denominado Ds32gt.dll convierte los valores de argumento de 16 bits pasados a través de un archivo DLL de instalación de 32 bits de nuevo a 16 bits.  
  
## <a name="components"></a>Componentes  
 El componente ODBC del SDK de MDAC 2.8 SP1 incluye los siguientes archivos para ejecutar aplicaciones de 16 bits con controladores de 32 bits. Estos componentes se encuentran en el directorio .Redist.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL de thunking genérico ODBC de 16 bits|  
|Odbc32gt.dll|DLL de 32 bits ODBC generic thunking|  
|Odbccp32.dll|DLL del instalador de 32 bits|  
|Odbcad32.exe|Programa de administrador de 32 bits|  
|Odbcinst.hlp|Archivo de Ayuda del instalador|  
|Ds16gt.dll|DLL genérica de configuración del controlador de 16 bits|  
|Ctl3d32.dll|Biblioteca de estilo de ventana tridimensional de 32 bits|  
  
 Además, los siguientes archivos junto con el Administrador de controladores ODBC 2.10 de 16 bits, que no forman parte de ODBC 3.51, son necesarios y deben instalarse con la aplicación de 16 bits.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc.dll|Administrador de controladores de 16 bits|  
|Odbcinst.dll|DLL del instalador de 16 bits|  
|Odbcadm.exe|Programa de administrador ODBC de 16 bits|
