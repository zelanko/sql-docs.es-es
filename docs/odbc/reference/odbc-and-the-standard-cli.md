---
title: ODBC y la CLI estándar ( Standard CLI) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], CLI
- CLI [ODBC]
- CLI [ODBC], about CLI
- call-level interface [ODBC]
- call-level interface [ODBC], about call-level interface
ms.assetid: 79b9c268-16ac-4b80-b451-f9dcd8c02ca4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 56dc0ac73c77cbbb77943d2e9ba308796b259dbb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305146"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC y la CLI estándar
ODBC se alinea con las siguientes especificaciones y estándares que se ocupan de la interfaz de nivel de llamada (CLI). (Las características ODBC son un superconjunto de cada uno de estos estándares.)  
  
-   La especificación CAE del grupo abierto "Administración de datos: Interfaz de nivel de llamada (CLI) SQL"  
  
-   Interfaz de nivel de llamada ISO/IEC 9075-3:1995 (E) (SQL/CLI)  
  
 Como resultado de esta alineación, se cumple lo siguiente:  
  
-   Una aplicación escrita en las especificaciones de Open Group e ISO CLI funcionará con un controlador ODBC *3.x* o un controlador compatible con estándares cuando se compila con los archivos de encabezado ODBC *3.x* y se vincula con bibliotecas ODBC *3.x* y cuando obtiene acceso al controlador a través del Administrador de controladores ODBC *3.x.*  
  
-   Un controlador escrito en las especificaciones de Open Group e ISO CLI funcionará con una aplicación ODBC *3.x* o una aplicación compatible con estándares cuando se compila con los archivos de encabezado ODBC *3.x* y se vincula con bibliotecas ODBC *3.x* y cuando la aplicación obtiene acceso al controlador a través del Administrador de controladores ODBC *3.x.* (Para obtener más información, consulte [Aplicaciones y controladores compatibles](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md)con estándares .  
  
 El nivel de conformidad de la interfaz principal abarca todas las características de la CLI ISO y todas las características no opcionales en la CLI del grupo abierto. Las características opcionales de la CLI del grupo abierto aparecen en los niveles de conformidad de la interfaz más altos. Dado que todos los controladores ODBC *3.x* son necesarios para admitir las características en el nivel de conformidad de la interfaz principal, se cumple lo siguiente:  
  
-   Un controlador ODBC *3.x* admitirá todas las características utilizadas por una aplicación compatible con estándares.  
  
-   Una aplicación ODBC *3.x* que solo usa las características de la CLI de ISO y las características no opcionales de la CLI de grupo abierto funcionará con cualquier controlador compatible con estándares.  
  
 Además de las especificaciones de interfaz de nivel de llamada contenidas en los estándares ISO/IEC y Open Group CLI, ODBC implementa las siguientes características. (Algunas de estas características existían en versiones de ODBC anteriores a ODBC *3.x*.)  
  
-   Capturas multifila mediante una sola llamada de función  
  
-   Enlace a una matriz de parámetros  
  
-   Compatibilidad con marcadores, incluida la obtención por marcadores, marcadores de longitud variable y operaciones de actualización y eliminación masivas de marcadores en filas no contiguas  
  
-   Enlace de modo de fila  
  
-   Desplazamientos de enlace  
  
-   Compatibilidad con lotes de instrucciones SQL, ya sea en un procedimiento almacenado o como una secuencia de instrucciones SQL ejecutadas a través de **SQLExecute** o **SQLExecDirect**  
  
-   Recuentos exactos o aproximados de filas de cursor  
  
-   Operaciones de actualización y eliminación posicionadas y actualizaciones y eliminaciones por lotes por llamada de función (**SQLSetPos**)  
  
-   Funciones de catálogo que extraen información del esquema de información sin necesidad de admitir vistas de esquema de información  
  
-   Secuencias de escape para combinaciones externas, funciones escalares, literales de fecha y hora, literales de intervalo y procedimientos almacenados  
  
-   Bibliotecas de traducción de páginas de códigos  
  
-   Informes del nivel de conformidad ANSI de un conductor y soporte SQL  
  
-   Población automática bajo demanda del descriptor de parámetros de implementación  
  
-   Diagnóstico mejorado y matrices de estado de filas y parámetros  
  
-   Tipos de búfer de aplicación de enteros de fecha, intervalo, numérico/decimal y 64 bits  
  
-   Ejecución asincrónica  
  
-   Compatibilidad con procedimientos almacenados, incluidas las secuencias de escape, los mecanismos de enlace de parámetros de salida y las funciones de catálogo  
  
-   Mejoras de conexión, incluida la compatibilidad con atributos de conexión y la exploración de atributos
