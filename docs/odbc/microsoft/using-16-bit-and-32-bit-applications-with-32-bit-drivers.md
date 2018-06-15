---
title: Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits | Documentos de Microsoft
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
- ODBC drivers [ODBC], 16-bit applications
- ODBC drivers [ODBC], 32-bit applications
- 32-bit applications with 32-bit drivers [ODBC]
- 16-bit applications with 32-bit drivers [ODBC]
ms.assetid: fc65c988-b31f-4cc9-851f-30d2119604fd
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 97f4224967cd0c54b134d118533ed66f6043762c
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32908920"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits
> [!IMPORTANT]  
>  compatibilidad con aplicaciones de 16 bits se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Desarrollar aplicaciones de 32 bits o 64 bits en su lugar.  
  
 Con el componente de acceso a datos ODBC, puede usar las aplicaciones de 16 bits y 32 bits con controladores de 32 bits. Sistemas operativos Microsoft® Windows® 95 ó 98 y Microsoft Windows/Windows 2000 admiten las siguientes combinaciones de aplicaciones y controladores:  
  
-   aplicaciones de 16 bits con controladores de 32 bits  
  
-   aplicaciones de 32 bits con controladores de 32 bits  
  
 No se admite el uso de una aplicación de 32 bits con un controlador de 16 bits.  
  
> [!NOTE]  
>  A partir de la versión de ODBC versión 3.0, Windows NT 4.0 compatible.  
  
 ODBC incluye los componentes ODBC necesarios para admitir las configuraciones anteriores "thunk" bibliotecas de vínculos dinámicos (DLL) para convertir las direcciones de 16 bits a direcciones de 32 bits y viceversa. El programa de instalación determina qué sistema operativo está usando e instala los componentes ODBC necesarios para ese sistema. También puede elegir instalar los componentes ODBC utilizados por todos los sistemas.  
  
 En la mayoría de los casos, al trasladar una aplicación o un controlador de 16 bits a 32 bits implica cinco tipos de cambios:  
  
-   Cambios en el código de control de mensajes  
  
-   Cambie porque enteros y los identificadores son de 32 bits  
  
-   Cambios en las llamadas a las interfaces de programación de aplicaciones (API) de Windows  
  
-   Cambios para que el controlador seguro para subprocesos  
  
-   Cambios en los componentes ODBC  
  
 Desde una perspectiva de programación aplicación o el controlador, la diferencia principal entre los componentes ODBC de 16 bits y 32 bits es que tienen diferentes nombres de archivo. Desde la perspectiva del sistema, la arquitectura de cada conexión de la aplicación o el controlador es diferente y las herramientas utilizadas para administrar orígenes de datos son diferentes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de las aplicaciones de 16 bits con controladores de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso de las aplicaciones de 32 bits con controladores de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
