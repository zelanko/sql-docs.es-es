---
title: Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 8540983b84d4d39fe5a02b92a1e3a3606350d36d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63209998"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits
> [!IMPORTANT]  
>  compatibilidad con aplicaciones de 16 bits se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Desarrollar aplicaciones de 32 bits o 64 bits en su lugar.  
  
 Con el componente de acceso de datos ODBC, puede usar las aplicaciones de 16 bits y 32 bits con controladores de 32 bits. Los sistemas operativos Microsoft® Windows® 95/98 y Microsoft Windows o Windows 2000 admiten las siguientes combinaciones de aplicaciones y controladores:  
  
-   aplicaciones de 16 bits con controladores de 32 bits  
  
-   aplicaciones de 32 bits con controladores de 32 bits  
  
 No se admite el uso de una aplicación de 32 bits con un controlador de 16 bits.  
  
> [!NOTE]  
>  Desde la versión de ODBC versión 3.0, se admite Windows NT 4.0.  
  
 ODBC incluye los componentes ODBC necesarios para admitir las configuraciones mencionadas anteriormente "thunk" bibliotecas de vínculos dinámicos (DLL) para convertir las direcciones de 16 bits a direcciones de 32 bits y viceversa. El programa de instalación determina qué sistema operativo que está usando e instala los componentes ODBC requeridos ese sistema. También puede instalar los componentes ODBC usados por todos los sistemas.  
  
 En la mayoría de los casos, trasladar una aplicación o un controlador de 16 bits a 32 bits implica cinco tipos de cambios:  
  
-   Cambios en el código de tratamiento de mensajes  
  
-   Cambia porque son identificadores y enteros de 32 bits  
  
-   Cambios en las llamadas a interfaces de programación de aplicaciones (API) de Windows  
  
-   Cambios para que el controlador seguro para subprocesos  
  
-   Cambios en los componentes ODBC  
  
 Desde una perspectiva de programación controlador o aplicación, la principal diferencia entre los componentes ODBC de 16 bits y 32 bits es que tienen nombres de archivo diferente. Desde la perspectiva del sistema, la arquitectura de cada conexión de la aplicación o el controlador es diferente y las herramientas utilizadas para administrar orígenes de datos son diferentes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de las aplicaciones de 16 bits con controladores de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso de las aplicaciones de 32 bits con controladores de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
