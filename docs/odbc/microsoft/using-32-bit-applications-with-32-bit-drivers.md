---
title: Uso de las aplicaciones de 32 bits con controladores de 32 bits | Documentos de Microsoft
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
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e37da481e8068edb966b8f8ace4f129989cce990
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 32 bits con controladores de 32 bits
Puede ejecutar aplicaciones de 32 bits con controladores de 32 bits. Las aplicaciones de 32 bits y los controladores de 32 bits utilizan la API Win32®.  
  
## <a name="architecture"></a>Architecture  
 La siguiente ilustración muestra las aplicaciones de 32 bits cómo comunicarse con los controladores de 32 bits. La aplicación llama al administrador de controladores de 32 bits, que a su vez llama a controladores de 32 bits.  
  
 ![Cómo 32 &#45; las aplicaciones de bits se comunican con 32 &#45; bit controladores](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  No utilice al instalador thunk DLL de 32 bits en Windows NT o Windows 2000. Aunque tiene el mismo nombre de archivo que el programa de instalación de 32 bits DLL, es una DLL diferente.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para controladores de 32 bits mediante el Administrador de orígenes de datos ODBC. Para abrir el Administrador de ODBC en equipos que ejecutan Windows 2000, abra el Panel de Control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)**. En equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC de 32 bits** o simplemente **ODBC**.  
  
## <a name="components"></a>Components  
 El componente ODBC incluye los siguientes archivos para ejecutar aplicaciones de 32 bits con controladores de 32 bits. Estos componentes se encuentran en el directorio \Redist.  
  
|Nombre de archivo|Description|  
|---------------|-----------------|  
|Odbc32.dll|Administrador de controladores de 32 bits|  
|Odbccp32.dll|DLL del instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de ODBC de 32 bits|  
|Odbcinst.hlp|Archivo de Ayuda del programa de instalación|  
|MSVCRT40.dll|Biblioteca en tiempo de ejecución de C|
