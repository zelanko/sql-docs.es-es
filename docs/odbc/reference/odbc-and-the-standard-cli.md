---
title: ODBC y la CLI estándar | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5222282bce2acf49cc6a144667ddd691528b3693
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "67944845"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC y la CLI estándar
ODBC se alinea con las siguientes especificaciones y estándares que se ocupan de la interfaz de nivel de llamada (CLI). (Las características ODBC son un superconjunto de cada una de estas normas).  
  
-   La especificación de Open Group CAE "Administración de datos: interfaz de nivel de llamada de SQL (CLI)"  
  
-   Interfaz de nivel de llamada ISO/IEC 9075-3:1995 (E) (SQL/CLI)  
  
 Como resultado de esta alineación, se cumplen las condiciones siguientes:  
  
-   Una aplicación escrita en las especificaciones Open Group e ISO CLI funcionará con un controlador ODBC *3. x* o con un controlador compatible con los estándares cuando se compila con los archivos de encabezado ODBC *3.* x y se vincula con bibliotecas ODBC *3. x* , y cuando obtiene acceso al controlador a través del administrador de controladores ODBC *3. x* .  
  
-   Un controlador escrito en las especificaciones Open Group e ISO CLI funcionará con una aplicación ODBC *3. x* o conforme a los estándares cuando se compila con los archivos de encabezado ODBC *3.* x y se vinculan a las bibliotecas ODBC *3. x* , y cuando la aplicación obtiene acceso al controlador a través del administrador de controladores ODBC *3. x* . (Para obtener más información, vea [aplicaciones y controladores compatibles con los estándares](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 El nivel de conformidad de la interfaz principal engloba todas las características de la CLI ISO y todas las características no opciones de la CLI de apertura de grupos. Las características opcionales de la CLI de grupo abierto aparecen en niveles de compatibilidad de interfaz más altos. Dado que todos los controladores ODBC *3. x* son necesarios para admitir las características en el nivel de conformidad de la interfaz principal, se cumplen las siguientes condiciones:  
  
-   Un controlador ODBC *3. x* admitirá todas las características que usa una aplicación compatible con los estándares.  
  
-   Una aplicación ODBC *3. x* que use solo las características de la CLI ISO y las características no opciones de la CLI Open Group funcionarán con cualquier controlador compatible con los estándares.  
  
 Además de las especificaciones de la interfaz de nivel de llamada contenidas en los estándares ISO/IEC y Open Group CLI, ODBC implementa las características siguientes. (Algunas de estas características existían en las versiones de ODBC anteriores a ODBC *3. x*).  
  
-   Una única llamada de función realiza capturas de varias filas  
  
-   Enlazar a una matriz de parámetros  
  
-   Compatibilidad con marcadores, incluida la captura por marcador, marcadores de longitud variable y actualización y eliminación masivas por operaciones de marcador en filas no contiguas  
  
-   Enlace de modo de fila  
  
-   Desplazamientos de enlace  
  
-   Compatibilidad con lotes de instrucciones SQL, ya sea en un procedimiento almacenado o como una secuencia de instrucciones SQL ejecutadas a través de **SQLExecute** o **SQLExecDirect**  
  
-   Recuentos de filas de cursor exactas o aproximadas  
  
-   Operaciones de actualización y eliminación posicionadas y actualizaciones por lotes y eliminaciones por llamada a función (**SQLSetPos**)  
  
-   Funciones de catálogo que extraen información del esquema de información sin necesidad de admitir las vistas de esquema de información  
  
-   Secuencias de escape para combinaciones externas, funciones escalares, literales de fecha y hora, literales de intervalo y procedimientos almacenados  
  
-   Bibliotecas de traducción de páginas de códigos  
  
-   Informes del nivel de conformidad con ANSI de un controlador y la compatibilidad con SQL  
  
-   Rellenado automático a petición de descriptor de parámetros de implementación  
  
-   Matrices mejoradas de estado de parámetros y filas y diagnósticos  
  
-   Tipos de búfer de aplicación de tipo entero DateTime, Interval, Numeric/decimal y 64 bits  
  
-   Ejecución asincrónica  
  
-   Compatibilidad con procedimientos almacenados, incluidas secuencias de escape, mecanismos de enlace de parámetros de salida y funciones de catálogo  
  
-   Mejoras en la conexión, incluida la compatibilidad con los atributos de conexión y la exploración de atributos
