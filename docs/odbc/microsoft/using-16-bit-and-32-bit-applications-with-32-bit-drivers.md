---
title: Uso de aplicaciones de 16 y 32 bits con controladores de 32 bits Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7ce996a7c4816d4d14491e226f891904b6cf8c02
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81307616"
---
# <a name="using-16-bit-and-32-bit-applications-with-32-bit-drivers"></a>Uso de las aplicaciones de 16 bits y 32 bits con controladores de 32 bits
> [!IMPORTANT]  
>  La compatibilidad con aplicaciones de 16 bits se eliminará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. Desarrolle aplicaciones de 32 o 64 bits en su lugar.  
  
 Con el componente de acceso a datos ODBC, puede utilizar aplicaciones de 16 y 32 bits con controladores de 32 bits. Los sistemas operativos Microsoft® Windows® 95/98 y Microsoft Windows NT®/Windows 2000 admiten las siguientes combinaciones de aplicaciones y controladores:  
  
-   Aplicaciones de 16 bits con controladores de 32 bits  
  
-   Aplicaciones de 32 bits con controladores de 32 bits  
  
 No se admite el uso de una aplicación de 32 bits con un controlador de 16 bits.  
  
> [!NOTE]  
>  A partir de la versión 3.0 de ODBC, se ha admitido Windows NT 4.0.  
  
 ODBC incluye los componentes ODBC necesarios para admitir las configuraciones anteriores mediante "thunking" bibliotecas de vínculos dinámicos (DLL) para convertir direcciones de 16 bits a direcciones de 32 bits y viceversa. El programa de instalación determina qué sistema operativo está utilizando e instala los componentes ODBC requeridos por ese sistema. También puede optar por instalar los componentes ODBC utilizados por todos los sistemas.  
  
 En la mayoría de los casos, la portabilidad de una aplicación o controlador de 16 bits a 32 bits implica cinco tipos de cambios:  
  
-   Cambios en el código de control de mensajes  
  
-   Cambios porque los enteros y los identificadores son 32 bits  
  
-   Cambios en las llamadas a interfaces de programación de aplicaciones de Windows (API)  
  
-   Cambios para que el controlador sea seguro para subprocesos  
  
-   Cambios en los componentes ODBC  
  
 Desde el punto de vista de la programación de aplicaciones o controladores, la principal diferencia entre los componentes ODBC de 16 bits y 32 bits es que tienen nombres de archivo diferentes. Desde el punto de vista del sistema, la arquitectura de cada conexión de aplicación o controlador es diferente y las herramientas utilizadas para administrar orígenes de datos son diferentes.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Uso de las aplicaciones de 16 bits con controladores de 32 bits](../../odbc/microsoft/using-16-bit-applications-with-32-bit-drivers.md)  
  
-   [Uso de las aplicaciones de 32 bits con controladores de 32 bits](../../odbc/microsoft/using-32-bit-applications-with-32-bit-drivers.md)
