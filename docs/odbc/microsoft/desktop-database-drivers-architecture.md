---
title: Arquitectura de controladores de base de datos de escritorio ( Desktop Database Drivers Architecture) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], architecture
- ODBC desktop database drivers [ODBC], architecture
- desktop database drivers [ODBC], architecture
ms.assetid: 8b4d13f7-ab37-40b4-a9c6-145e7385352f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ae6fb72bb3ed0a9bca1571eb572bbfbd20fe9995
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288745"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitectura de controladores de escritorio de la base de datos
Estos controladores están diseñados para su uso en Microsoft Windows 95 o posterior, o Windows NT 4.0 y Windows 2000. Solo las aplicaciones de 32 bits son compatibles con Windows 95 o posterior; Las aplicaciones de 16 y 32 bits son compatibles con Windows NT 4.0 y Windows 2000.  
  
> [!NOTE]  
>  Para obtener información acerca de la versión de ODBC que se usará con estos controladores, consulte la *referencia del programador ODBC*y las notas de la versión pasada y actual. A excepción de las áreas indicadas, estos controladores se ajustan a la *referencia del programador ODBC*.  
  
 Los controladores de base de datos de escritorio ODBC incluyen controladores de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox y texto. No se incluyen controladores de 16 bits. (Un controlador para Microsoft FoxPro está disponible por separado.)  
  
 La arquitectura de aplicación/controlador en Windows 95 o posterior es:  
  
 ![Arquitectura del controlador de&#47;de aplicaciones: Windows 95 y versiones posteriores](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetarch1")  
  
 No se admite el uso de estos controladores por aplicaciones de 16 bits en Windows 95.  
  
 La arquitectura de aplicación/controlador en Windows NT 4.0 y Windows 2000 es:  
  
 ![Arquitectura del controlador de&#47;de aplicaciones: NT 4.0 y Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Los controladores de base de datos de escritorio son controladores de dos niveles. En una configuración de dos niveles, el controlador no realiza el proceso de análisis, validación, optimización y ejecución de la consulta. En su lugar, Microsoft Jet realiza estas tareas. Procesa las llamadas a la API ODBC y actúa como motor SQL. Microsoft Jet se ha convertido en una parte integral e inseparable de los controladores: Se suministra con los controladores y reside con los controladores, incluso si ninguna otra aplicación en el equipo lo utiliza.  
  
 Los controladores de base de datos de escritorio constan de seis controladores diferentes o, más precisamente, un archivo de controlador (Odbcjt32.dll) que el Administrador de [controladores](../../odbc/reference/the-driver-manager.md) ODBC utiliza de seis maneras diferentes. La marca DRIVERID en la entrada del Registro para un origen de datos determina qué controlador de Odbcjt32.dll utiliza el Administrador de controladores. Una aplicación pasa esta marca en la cadena de conexión incluida en una llamada a **SQLDriverConnect**. De forma predeterminada, la marca es el identificador del controlador de Microsoft Access.  
  
 El archivo de configuración del controlador cambia la marca DRIVERID en el momento de la configuración. Todos los controladores excepto el controlador de Microsoft Access tienen un archivo DLL de instalación asociado. Al hacer clic en **Configurar** en el Administrador de orígenes de [datos ODBC](../../odbc/admin/odbc-data-source-administrator.md) de Microsoft para un origen de datos, el archivo DLL del instalador ODBC (Odbcinst.dll) carga el archivo DLL de instalación. El archivo DLL de instalación exporta la función de instalador ODBC **SQLConfigDataSource**. Si se pasa un identificador de ventana a **SQLConfigDataSource**, esta función muestra una ventana de configuración y cambia el indicador DRIVERID según el controlador seleccionado en la interfaz de usuario.  
  
 Cuando se crea un archivo mediante programación, se pasa un identificador de ventana NULL a **SQLConfigDataSource**y la función crea un origen de datos dinámicamente, cambiando el indicador DRIVERID según el argumento *lpszDriver* en la llamada de función.  
  
 Odbcjt32.dll implementa funciones ODBC en la parte superior de la API de Microsoft Jet. Sin embargo, no hay ninguna asignación directa entre las funciones ODBC y Microsoft Jet. Muchos factores, como los modelos de cursor y la asignación SQL, impiden una correlación directa de las funciones.  
  
 El controlador ODBC reside entre el motor de Microsoft Jet y el Administrador de controladores ODBC. Algunas funciones ODBC a las que llama una aplicación las controla el Administrador de controladores y no se pasan al controlador. Para estas funciones, Microsoft Jet nunca ve la llamada de función porque no tiene una conexión directa con el Administrador de controladores.
