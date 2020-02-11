---
title: Usar aplicaciones de 16 y 32 bits con controladores de 32 bits | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 941c821d7622b2364ec1cd417dd9b50302540b95
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68088172"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits
> [!IMPORTANT]  
>  la compatibilidad con aplicaciones de 16 bits se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Desarrolle aplicaciones de 32 bits o de 64 bits en su lugar.  
  
 Con el componente de acceso a datos ODBC, puede usar las aplicaciones de 16 bits y 32 bits con controladores de 32 bits. Los sistemas operativos Microsoft® Windows® 95/98 y Microsoft Windows NT®/Windows 2000 admiten las siguientes combinaciones de aplicaciones y controladores:  
  
-   aplicaciones de 16 bits con controladores de 32 bits  
  
-   aplicaciones de 32 bits con controladores de 32 bits  
  
 No se admite el uso de una aplicación de 32 bits con un controlador de 16 bits.  
  
> [!NOTE]  
>  A partir de la versión de ODBC 3,0, se admite Windows NT 4,0.  
  
 ODBC incluye los componentes ODBC necesarios para admitir las configuraciones anteriores por las bibliotecas de vínculos dinámicos (dll) de "thunk" para convertir direcciones de 16 bits en direcciones de 32 bits y viceversa. El programa de instalación determina qué sistema operativo se está usando e instala los componentes ODBC que requiere ese sistema. También puede optar por instalar los componentes ODBC utilizados por todos los sistemas.  
  
 En la mayoría de los casos, la migración de una aplicación o un controlador de 16 a 32 bits conlleva cinco tipos de cambios:  
  
-   Cambios en el código de control de mensajes  
  
-   Cambios porque los enteros y los identificadores son de 32 bits  
  
-   Cambios en las llamadas a interfaces de programación de aplicaciones (API) de Windows  
  
-   Cambios para que el controlador sea seguro para subprocesos  
  
-   Cambios en los componentes ODBC  
  
 Desde el punto de vista de la programación de una aplicación o un controlador, la diferencia principal entre los componentes ODBC de 16 y 32 bits es que tienen nombres de archivo diferentes. Desde el punto de vista del sistema, la arquitectura de cada conexión de aplicación o controlador es diferente y las herramientas que se usan para administrar los orígenes de datos son diferentes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de las aplicaciones de 16 bits con controladores de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso de las aplicaciones de 32 bits con controladores de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
