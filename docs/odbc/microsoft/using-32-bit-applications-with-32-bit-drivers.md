---
title: Uso de las aplicaciones de 32 bits con controladores de 32 bits | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
ms.assetid: 0cdd5788-5642-4280-8d53-b4ec461aafa1
caps.latest.revision: 13
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7a07dae46125ce9ea04bfc36156d8855192396f3
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32906440"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 32 bits con controladores de 32 bits
Puede ejecutar aplicaciones de 32 bits con controladores de 32 bits. Las aplicaciones de 32 bits y los controladores de 32 bits utilizan la API Win32®.  
  
## <a name="architecture"></a>Architecture  
 La siguiente ilustración muestra las aplicaciones de 32 bits cómo comunicarse con los controladores de 32 bits. La aplicación llama al administrador de controladores de 32 bits, que a su vez llama a controladores de 32 bits.  
  
 ![Cómo 32&#45;aplicaciones bits se comunican con 32&#45;bit controladores](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
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
