---
title: Arquitectura de controladores de base de datos de escritorio | Microsoft Docs
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
ms.openlocfilehash: ccd1f14b0cfbcbdbc675a142ebabf11932409832
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071909"
---
# <a name="desktop-database-drivers-architecture"></a>Arquitectura de controladores de escritorio de la base de datos
Estos controladores están diseñados para su uso en Microsoft Windows 95 o posterior, o en Windows NT 4,0 y Windows 2000. Solo se admiten aplicaciones de 32 bits en Windows 95 o posterior; las aplicaciones de 16 y 32 bits se admiten en Windows NT 4,0 y Windows 2000.  
  
> [!NOTE]  
>  Para obtener información acerca de la versión de ODBC que se va a usar con estos controladores, consulte la *Referencia del programador de ODBC*y las notas de la versión anterior y actual. A excepción de las áreas indicadas, estos controladores se ajustan a la *Referencia del programador de ODBC*.  
  
 Los controladores de base de datos de escritorio ODBC incluyen controladores de 32 bits para Microsoft Access, dBASE, Microsoft Excel, Paradox y texto. No se incluyen controladores de 16 bits. (Un controlador de Microsoft FoxPro está disponible por separado).  
  
 La arquitectura de aplicaciones y controladores en Windows 95 o posterior es:  
  
 ![Arquitectura de controladores de&#47;de aplicaciones: Windows 95 y versiones posteriores](../../odbc/microsoft/media/odbcjetarch1.gif "ODBCJetArch1")  
  
 No se admite el uso de estos controladores por parte de aplicaciones de 16 bits en Windows 95.  
  
 La arquitectura de aplicaciones y controladores en Windows NT 4,0 y Windows 2000 es:  
  
 ![Arquitectura de controladores de&#47;de aplicaciones: NT 4,0 y Windows 2000](../../odbc/microsoft/media/odbcjetarch2.gif "ODBCJetArch2")  
  
 Los controladores de base de datos de escritorio son controladores de dos niveles. En una configuración de dos niveles, el controlador no realiza el proceso de análisis, validación, optimización y ejecución de la consulta. En su lugar, Microsoft Jet realiza estas tareas. Procesa las llamadas a la API de ODBC y actúa como un motor SQL. Microsoft Jet se ha convertido en una parte integral e inseparable de los controladores: se incluye con los controladores y reside en los controladores, incluso si ninguna otra aplicación del equipo lo usa.  
  
 Los controladores de base de datos de escritorio constan de seis controladores distintos (o, más concretamente, un archivo de controlador (Odbcjt32. dll) que usa el [Administrador de controladores](../../odbc/reference/the-driver-manager.md) ODBC de seis maneras diferentes. La marca DRIVERID de la entrada del registro para un origen de datos determina qué controlador de Odbcjt32. dll utiliza el administrador de controladores. Una aplicación pasa esta marca en la cadena de conexión incluida en una llamada a **SQLDriverConnect**. De forma predeterminada, la marca es el identificador del controlador de Microsoft Access.  
  
 El archivo de instalación del controlador cambia la marca DRIVERID en el momento de la instalación. Todos los controladores excepto el controlador de Microsoft Access tienen una DLL de instalación asociada. Al hacer clic en **configurar** en el [Administrador de orígenes de datos ODBC de Microsoft](../../odbc/admin/odbc-data-source-administrator.md) para un origen de datos, el archivo DLL del instalador de ODBC (Odbcinst. DLL) carga el archivo dll de instalación. El archivo DLL de instalación exporta la función del instalador de ODBC **SQLConfigDataSource**. Si se pasa un identificador de ventana a **SQLConfigDataSource**, esta función muestra una ventana de configuración y cambia la marca DRIVERID según el controlador seleccionado en la interfaz de usuario.  
  
 Cuando un archivo se crea mediante programación, se pasa un identificador de ventana nulo a **SQLConfigDataSource**y la función crea un origen de datos dinámicamente, cambiando la marca DRIVERID según el argumento *lpszDriver* en la llamada de función.  
  
 Odbcjt32. dll implementa funciones ODBC sobre la API de Microsoft Jet. Sin embargo, no hay ninguna asignación directa entre las funciones ODBC y Microsoft Jet. Muchos factores, como los modelos de cursor y la asignación de SQL, impiden una correlación directa de las funciones.  
  
 El controlador ODBC reside entre el motor de Microsoft Jet y el administrador de controladores ODBC. Algunas funciones ODBC llamadas por una aplicación las controla el administrador de controladores y no se pasan al controlador. Para estas funciones, Microsoft Jet nunca ve la llamada de función porque no tiene una conexión directa con el administrador de controladores.
