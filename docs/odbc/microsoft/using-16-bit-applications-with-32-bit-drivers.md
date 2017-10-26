---
title: Uso de las aplicaciones de 16 bits con controladores de 32 bits | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: 68feb3b7-c01a-4f42-8df9-f9c182d89325
caps.latest.revision: 12
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d35585ec95bdfed62c527dfe004132c7454e5243
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-16-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits con controladores de 32 bits
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y piense en modificar las aplicaciones que actualmente utilizan esta característica. Utilice el Administrador de controladores de 32 bits o 64 bits en su lugar.  
  
 Puede ejecutar aplicaciones de 16 bits con controladores de 32 bits en un sistema basado en Windows como el controlador de 32 bits no se llama explícitamente a funciones de la API de Win32 que crean subprocesos. El subsistema Windows on Windows (WOW) ejecuta las aplicaciones en modo de 16 bits y resuelve las llamadas de 16 bits en el sistema operativo. ODBC thunk llamadas de 16 bits de resolución de DLL desde la aplicación a los controladores de 32 bits. Las aplicaciones de 16 bits utilizan la API de Windows y controladores de 32 bits utilizan la API de Win32.  
  
## <a name="architecture"></a>Architecture  
 En la siguiente ilustración muestra las aplicaciones de 16 bits cómo comunicarse con los controladores de 32 bits. Entre el Administrador de controladores de 16 bits y los controladores de 32 bits que son genéricas thunk DLL que convertir las llamadas ODBC de 16 bits a las llamadas ODBC de 32 bits.  
  
 ![Cómo 16 &#45; las aplicaciones de bits se comunican con 32 &#45; bit controladores](../../odbc/microsoft/media/sdka2.gif "sdka2")  
  
> [!NOTE]  
>  Cada vez que una aplicación de 16 bits interactúa con un controlador de 32 bits, el Administrador de controladores de 32 bits siempre devuelve "2.0" como la versión de ODBC compatibles con el controlador.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para controladores de 32 bits mediante el Administrador de orígenes de datos ODBC. Para abrir el Administrador de ODBC en equipos que ejecutan Microsoft® Windows® 2000, abra el Panel de Control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. En equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC de 32 bits** o simplemente **ODBC**.  
  
 La ilustración siguiente muestra cómo una aplicación de 16 bits llama a un archivo DLL de configuración de controladores de 32 bits. Entre el archivo DLL de instalador de 16 bits y el controlador de 32 bits archivo DLL de configuración es una DLL thunk genérica que convierte las llamadas a DLL instalador de 16 bits en llamadas DLL de instalador de 32 bits.  
  
 ![Cómo un 16 &#45; bit aplicación llama a un 32 &#45; bit DLL de instalación de controlador](../../odbc/microsoft/media/sdka3.gif "sdka3")  
  
 En Windows on Windows (thunk de 16 bits a 32 bits), una DLL thunk adicional denominada convierte Ds32gt.dll valores de argumento de 16 bits se pasan a través de un programa de instalación de 32 bits DLL de nuevo al 16 bits.  
  
## <a name="components"></a>Components  
 El componente ODBC de los SDK de MDAC 2.8 SP1 incluye los siguientes archivos para ejecutar aplicaciones de 16 bits con controladores de 32 bits. Estos componentes se encuentran en el directorio \Redist.  
  
|Nombre de archivo|Description|  
|---------------|-----------------|  
|Odbc16gt.dll|DLL thunk de 16 bits ODBC genérico|  
|Odbc32gt.dll|DLL de 32 bits ODBC genérico thunk|  
|Odbccp32.dll|DLL del instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de 32 bits|  
|Odbcinst.hlp|Archivo de Ayuda del programa de instalación|  
|Ds16gt.dll|instalación del controlador de 16 bits genérica thunk DLL|  
|Archivo Ctl3d32.dll|biblioteca de estilos de ventana tridimensional de 32 bits|  
  
 Además, los archivos siguientes junto con el Administrador de controladores de 2.10 de ODBC de 16 bits, que no forman parte de ODBC 3.51, requieren y deben instalarse con la aplicación de 16 bits.  
  
|Nombre de archivo|Description|  
|---------------|-----------------|  
|ODBC.dll|Administrador de controladores de 16 bits|  
|Odbcinst.dll|Instalador de 16 bits DLL|  
|Odbcadm.exe|programa de administrador de ODBC de 16 bits|

