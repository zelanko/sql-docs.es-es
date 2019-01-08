---
title: Arquitectura de controladores de escritorio de la base de datos | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7487d073b95190418ee7f6900390a2d60ce42e13
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52516867"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitectura de controladores de escritorio de la base de datos
Estos controladores están diseñados para uso en Microsoft Windows 95 o versiones posteriores, o Windows NT 4.0 y Windows 2000. Las aplicaciones de 32 bits sola se admiten en Windows 95 o versiones posteriores; se admiten las aplicaciones de 16 bits y 32 bits en Windows NT 4.0 y Windows 2000.  
  
> [!NOTE]  
>  Para obtener información acerca de la versión de ODBC para su uso con estos controladores, consulte el *referencia del programador de ODBC*y notas de la versión actual y antiguo. Excepto en las áreas indicadas, estos controladores se ajustan a la *referencia del programador de ODBC*.  
  
 Los controladores de base de datos ODBC Desktop incluir controladores de 32 bits de Microsoft Excel, texto, dBASE, Microsoft Access y Paradox. Los controladores de bits de 16 - no se incluyen. (Un controlador de Microsoft FoxPro está disponible por separado).  
  
 La arquitectura de aplicaciones y controladores en Windows 95 o versiones posteriores es:  
  
 ![Aplicación&#47;arquitectura de controladores: Windows 95 y posterior](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 No se admite el uso de estos controladores, las aplicaciones de 16 bits en Windows 95.  
  
 La arquitectura de aplicaciones y controladores en Windows NT 4.0 y Windows 2000 es:  
  
 ![Aplicación&#47;arquitectura de controladores: NT 4.0 y Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Los controladores de base de datos de escritorio son dos niveles. En una configuración de dos niveles, el controlador no realiza el proceso de análisis, validación, optimizar y ejecutar la consulta. En su lugar, Microsoft Jet realiza estas tareas. Procesa las llamadas de API de ODBC y actúa como un motor SQL. Microsoft Jet se ha convertido en una parte integral, inseparable de los controladores: Se incluye con los controladores y reside con los controladores, incluso si lo no usa ninguna otra aplicación en el equipo.  
  
 Los controladores de base de datos de escritorio constan de distintos seis controladores - o, más concretamente, uno (Odbcjt32.dll) del archivo de controlador que ODBC [Administrador de controladores](../../odbc/reference/the-driver-manager.md) usa seis maneras diferentes. La marca DRIVERID en la entrada del registro para un origen de datos determina qué controlador en Odbcjt32.dll se utiliza el Administrador de controladores. Una aplicación pasa esta marca en la cadena de conexión incluida en una llamada a **SQLDriverConnect**. De forma predeterminada, la marca es el identificador del controlador de Microsoft Access.  
  
 El archivo de instalación del controlador cambia la marca DRIVERID durante la instalación. Todos los controladores, excepto el controlador de Microsoft Access tienen un archivo DLL de configuración asociada. Al hacer clic en **instalación** en el [Administrador de orígenes de datos ODBC de Microsoft](../../odbc/admin/odbc-data-source-administrator.md) para un origen de datos, el programa de instalación ODBC DLL (Odbcinst.dll) carga el archivo DLL de configuración. El programa de instalación de DLL exporta la función del instalador ODBC **SQLConfigDataSource**. Si se pasa un identificador de ventana a **SQLConfigDataSource**, esta función muestra una ventana de configuración y cambia la marca DRIVERID según el controlador seleccionado desde la interfaz de usuario.  
  
 Cuando se crea un archivo mediante programación, se pasa un identificador de ventana NULL a **SQLConfigDataSource**, y la función crea un origen de datos de forma dinámica, cambiar el indicador DRIVERID según el *lpszDriver*argumento en la llamada de función.  
  
 Odbcjt32.dll implementa funciones ODBC en la API de Microsoft Jet. Sin embargo, hay ninguna asignación directa entre las funciones de ODBC y Microsoft Jet. Muchos factores, como los modelos de cursor y la asignación de SQL, evitar una correlación directa de las funciones.  
  
 El controlador ODBC se encuentra entre el motor Microsoft Jet y el Administrador de controladores ODBC. Algunas funciones ODBC llamadas a una aplicación son controladas por el Administrador de controladores y no se pasan al controlador. Para estas funciones, Microsoft Jet nunca ve la función llamar porque no tiene una conexión directa al administrador de controladores.
