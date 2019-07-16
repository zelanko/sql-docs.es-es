---
title: Uso de las aplicaciones de 32 bits con controladores de 32 bits | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 6b4d14cc65b31a0641149ace931efe46c914ad1b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68088164"
---
# <a name="using-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 32 bits con controladores de 32 bits
Puede ejecutar aplicaciones de 32 bits con controladores de 32 bits. Las aplicaciones de 32 bits y los controladores de 32 bits usan la API Win32®.  
  
## <a name="architecture"></a>Arquitectura  
 La siguiente ilustración muestra las aplicaciones de 32 bits cómo comunicarse con los controladores de 32 bits. La aplicación llama el Administrador de controladores de 32 bits, que a su vez llama a los controladores de 32 bits.  
  
 ![Cómo 32&#45;las aplicaciones de bits se comunican con 32&#45;bit controladores](../../odbc/microsoft/media/sdka6.gif "sdka6")  
  
> [!IMPORTANT]  
>  No utilice al instalador thunk DLL de 32 bits en Windows NT o Windows 2000. Aunque tiene el mismo nombre de archivo que la DLL de instalador de 32 bits, es una DLL diferente.  
  
## <a name="administration"></a>Administración  
 Puede administrar orígenes de datos para los controladores de 32 bits mediante el Administrador de orígenes de datos ODBC. Para abrir el Administrador de ODBC en equipos que ejecutan Windows 2000, abra el Panel de Control de Windows, haga doble clic en **herramientas administrativas**y, a continuación, haga doble clic en **orígenes de datos (ODBC)** . En equipos que ejecutan versiones anteriores de Microsoft Windows, el icono se denomina **ODBC 32-bit** o simplemente **ODBC**.  
  
## <a name="components"></a>Componentes  
 El componente ODBC incluye los siguientes archivos para ejecutar aplicaciones de 32 bits con controladores de 32 bits. Estos componentes están en el directorio \Redist.  
  
|Nombre de archivo|Descripción|  
|---------------|-----------------|  
|Odbc32.dll|Administrador de controladores de 32 bits|  
|Odbccp32.dll|DLL de instalador de 32 bits|  
|Odbcad32.exe|programa de administrador de ODBC de 32 bits|  
|Odbcinst.hlp|Archivo de Ayuda del instalador|  
|Msvcrt40.dll|Biblioteca de tiempo de ejecución de C|
