---
title: ODBC y la CLI estándar | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef863329a0f0c8a7c7b8aaef6f55717fbbc1f638
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="odbc-and-the-standard-cli"></a>ODBC y la CLI estándar
ODBC se alinea con las siguientes especificaciones y estándares que tratan con la interfaz de nivel de llamada (CLI). (Las características ODBC son un superconjunto de cada uno de estos estándares).  
  
-   La especificación de Open Group CAE "administración de datos: interfaz de nivel de llamada (CLI) de SQL"  
  
-   ISO/IEC 9075-interfaz de nivel de llamada 3:1995 (E) (SQL/CLI)  
  
 Como resultado de esta alineación, las siguientes afirmaciones son ciertas:  
  
-   Una aplicación escrita en las especificaciones de ISO CLI y Open Group funcionará con una aplicación ODBC 3. *x* controlador o un controlador compatible con los estándares cuando se compila con ODBC 3. *x* archivos de encabezado y vincular con ODBC 3. *x* bibliotecas, y cuando obtiene acceso al controlador a través de ODBC 3. *x* el Administrador de controladores.  
  
-   Un controlador que se escriben en las especificaciones de Open Group y ISO CLI funcionará con una aplicación ODBC 3*.x* aplicación o una aplicación compatible con los estándares cuando se compila con ODBC 3*.x* archivos de encabezado y vincular con ODBC 3*.x* bibliotecas, y cuando la aplicación obtiene acceso al controlador a través de ODBC 3*.x* el Administrador de controladores. (Para obtener más información, consulte [controladores y aplicaciones compatibles con los estándares](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 El nivel de conformidad de interfaz principal incluye todas las características de la CLI de ISO y todas las características no opcionales de la CLI de grupo abierto. Características opcionales de la CLI de grupo abierto aparecen en niveles más altos de conformidad de interfaz. Dado que todos los ODBC 3. *x* controladores son necesarios para admitir las características en el nivel de conformidad de interfaz de núcleos, lo siguiente es verdadero:  
  
-   Un ODBC 3. *x* controlador será compatible con todas las características usadas por una aplicación compatible con los estándares.  
  
-   Un ODBC 3. *x* aplicación usando solo las características de ISO CLI y las características no opcionales de la CLI de grupo abierto funcionará con cualquier controlador compatible con los estándares.  
  
 Además de las especificaciones de la interfaz de nivel de llamada contenidas en los estándares ISO/IEC y abra CLI de grupo, ODBC implementa las características siguientes. (Algunas de estas características existían en versiones de ODBC antes de ODBC 3. *x*.)  
  
-   Capturas de varias filas mediante una llamada de función única  
  
-   Enlazar a una matriz de parámetros  
  
-   Compatibilidad con marcadores incluidos por marcador, marcadores de longitud variable y masiva de filas, actualizar y eliminar operaciones de marcador en filas no contiguas  
  
-   Enlace de modo de fila  
  
-   Desplazamientos de enlace  
  
-   Compatibilidad con lotes de instrucciones SQL, ya sea en un procedimiento almacenado o como una secuencia de instrucciones SQL ejecutadas a través de **SQLExecute** o **SQLExecDirect**  
  
-   Recuentos de filas del cursor exacto o aproximado  
  
-   Coloca la actualización y las operaciones de eliminación y por lotes las actualizaciones y eliminaciones por llamada de función (**SQLSetPos**)  
  
-   Funciones de catálogo que extraen información del esquema de información sin necesidad de admitir vistas de esquema de información  
  
-   Secuencias de escape para procedimientos almacenados, funciones escalares, literales de fecha y hora, literales de intervalo y combinaciones externas  
  
-   Bibliotecas de traducción de páginas de códigos  
  
-   Creación de informes de un controlador, el nivel de conformidad con ANSI y soporte técnico SQL  
  
-   Rellenado automático a petición del descriptor de parámetro de implementación  
  
-   Diagnósticos mejorados y matrices de estado de fila y los parámetros  
  
-   Fecha y hora, de intervalo, numérico o decimal y tipos de búfer de aplicación de entero de 64 bits  
  
-   Ejecución asincrónica  
  
-   Compatibilidad con los procedimientos almacenados, incluidas las secuencias de escape, mecanismos de enlace de parámetro de salida y las funciones de catálogo  
  
-   Mejoras de conexión, incluida la compatibilidad para los atributos de conexión y examinar los atributos
