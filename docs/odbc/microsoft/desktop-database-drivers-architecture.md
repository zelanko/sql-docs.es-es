---
title: Arquitectura de controladores de escritorio de la base de datos | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0b85711437c50ccc246ad1af1432d9475d1cfc3d
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="desktop-database-drivers-architecture"></a>Arquitectura de controladores de escritorio de la base de datos
Estos controladores están diseñados para uso en Microsoft Windows 95 o una versión posterior, o Windows NT 4.0 y Windows 2000. Solo las aplicaciones de 32 bits se admiten en Windows 95 o versiones posteriores; se admiten las aplicaciones de 16 bits y 32 bits en Windows NT 4.0 y Windows 2000.  
  
> [!NOTE]  
>  Para obtener información acerca de la versión de ODBC que se utilizará con estos controladores, consulte el *referencia del programador de ODBC*y notas de la versión anterior y actual. Excepto en áreas anotadas, estos controladores se ajustan a la *referencia del programador de ODBC*.  
  
 Los controladores de base de datos de escritorio ODBC incluyen controladores de 32 bits de Microsoft Access, dBASE, Microsoft Excel, Paradox y de texto. Controladores de bits de 16 - no se incluyen. (Un controlador de Microsoft FoxPro está disponible por separado).  
  
 Es la arquitectura de aplicaciones y controladores en Windows 95 o versiones posteriores:  
  
 ![Aplicación &#47; arquitectura de controladores: Windows 95 y versiones posteriores](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 No se admite el uso de estos controladores por las aplicaciones de 16 bits en Windows 95.  
  
 La arquitectura de aplicación/controlador en Windows NT 4.0 y Windows 2000 es:  
  
 ![Aplicación &#47; arquitectura de controladores: NT 4.0 y Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Los controladores de base de datos de escritorio son dos niveles. En una configuración de dos niveles, el controlador no realiza el proceso de análisis, validación, optimizar y ejecutar la consulta. En su lugar, Microsoft Jet realiza estas tareas. Procesa las llamadas de API de ODBC y actúa como un motor SQL. Microsoft Jet se ha convertido en una parte integral, no separable de los controladores: que se incluye con los controladores y reside con los controladores, incluso si lo no usa ninguna otra aplicación en el equipo.  
  
 Los controladores de base de datos de escritorio consisten en seis distintos controladores, o, más concretamente, un controlador de archivo (Odbcjt32.dll) que ODBC [el Administrador de controladores](../../odbc/reference/the-driver-manager.md) usa de seis formas distintas. La marca DRIVERID en la entrada del registro para un origen de datos determina qué controlador en Odbcjt32.dll que utiliza el Administrador de controladores. Una aplicación pasa esta marca en la cadena de conexión que se incluyen en una llamada a **SQLDriverConnect**. De forma predeterminada, la marca es el identificador del controlador de Microsoft Access.  
  
 El archivo de instalación de controlador, cambia la marca DRIVERID durante la instalación. Todos los controladores excepto el controlador de Microsoft Access tienen un archivo DLL de configuración asociado. Al hacer clic en **el programa de instalación** en el [Administrador de orígenes de datos de Microsoft ODBC](../../odbc/admin/odbc-data-source-administrator.md) para un origen de datos, el programa de instalación ODBC DLL (Odbcinst.dll) carga el archivo DLL de configuración. El programa de instalación DLL exporta la función del instalador ODBC **SQLConfigDataSource**. Si se pasa un identificador de ventana al **SQLConfigDataSource**, esta función muestra una ventana de instalación y cambia la marca DRIVERID según el controlador seleccionado desde la interfaz de usuario.  
  
 Cuando se crea mediante programación un archivo, se pasa un identificador de ventana NULL a **SQLConfigDataSource**, y la función crea un origen de datos dinámicamente, cambiar el indicador DRIVERID según el *lpszDriver*argumento en la llamada de función.  
  
 Odbcjt32.dll implementa funciones ODBC encima de la API de Microsoft Jet. No hay ninguna asignación directa entre las funciones ODBC y Jet de Microsoft, sin embargo. Muchos factores, como los modelos de cursor y la asignación de SQL, evitar que una correlación directa de las funciones.  
  
 El controlador ODBC se encuentra entre el motor de Microsoft Jet y el Administrador de controladores ODBC. Algunas funciones ODBC llamadas a una aplicación se controla por el Administrador de controladores y no pasan al controlador. Para estas funciones, Microsoft Jet nunca ve la función llama a porque no tiene una conexión directa al administrador de controladores.

