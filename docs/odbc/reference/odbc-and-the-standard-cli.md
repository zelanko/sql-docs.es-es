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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67944845"
---
# <a name="odbc-and-the-standard-cli"></a>ODBC y la CLI estándar
ODBC se alinea con las siguientes especificaciones y estándares que tratan con la interfaz de nivel de llamada (CLI). (Las funciones ODBC son un superconjunto de cada uno de estos estándares).  
  
-   La especificación de Open Group CAE "administración de datos: Interfaz de nivel de llamada SQL (CLI)"  
  
-   ISO/IEC 9075-3:1995 (E) interfaz de nivel de llamada (SQL/CLI)  
  
 Como resultado de esta alineación, las siguientes afirmaciones son ciertas:  
  
-   Una aplicación creada a las especificaciones de Open Group y ISO CLI funcionará con un ODBC *3.x* controlador o un controlador compatible con los estándares cuando se compila con ODBC *3.x* archivos de encabezado y enlazan con ODBC *3.x* bibliotecas, y cuando obtiene acceso al controlador a través de ODBC *3.x* Administrador de controladores.  
  
-   Un controlador que se escriben en las especificaciones de Open Group y ISO CLI funcionará con un ODBC *3.x* aplicación o una aplicación estándar cuando se compila con ODBC *3.x* archivos de encabezado y vinculado con ODBC *3.x* bibliotecas, y cuando la aplicación obtiene acceso al controlador a través de ODBC *3.x* Administrador de controladores. (Para obtener más información, consulte [controladores y aplicaciones compatibles con estándares](../../odbc/reference/develop-app/standards-compliant-applications-and-drivers.md).  
  
 El nivel de conformidad de interfaz Core abarca todas las características de la CLI de ISO y todas las características no opcionales de la CLI de grupo abierto. Características opcionales de la CLI de grupo abierto aparecen en los niveles más altos de conformidad de interfaz. Dado que ODBC todas *3.x* controladores son necesarios para admitir las características en el nivel de conformidad de interfaz de núcleo, los siguientes son verdaderas:  
  
-   Un ODBC *3.x* controlador será compatible con todas las características usadas por una aplicación compatible con los estándares.  
  
-   Un ODBC *3.x* aplicación utilizando sólo las características de ISO CLI y las funciones no opcionales de la CLI de grupo abierto funcionará con cualquier controlador compatible con los estándares.  
  
 Además de las especificaciones de interfaz de nivel de llamada contenidas en los estándares ISO/IEC y la CLI de grupo abierta, ODBC implementa las características siguientes. (Algunas de estas características existían en versiones de ODBC antes de ODBC *3.x*.)  
  
-   Capturas de varias filas mediante una llamada de función única  
  
-   Enlazar a una matriz de parámetros  
  
-   Compatibilidad con marcadores incluidos capturando por marcador, los marcadores de longitud variable y bulk update y delete por las operaciones de marcador en filas no contiguas  
  
-   Enlace de modo de fila  
  
-   Desplazamientos de enlace  
  
-   Compatibilidad con lotes de instrucciones SQL, en un procedimiento almacenado o como una secuencia de instrucciones SQL ejecutadas a través de **SQLExecute** o **SQLExecDirect**  
  
-   Recuentos de filas del cursor exacto o aproximado  
  
-   Coloca la actualización y las operaciones de eliminación y por lotes de las actualizaciones y eliminaciones por llamada de función (**SQLSetPos**)  
  
-   Funciones de catálogo que extracción la información del esquema de información sin necesidad de compatibilidad con vistas de esquema de información  
  
-   Secuencias de escape para procedimientos almacenados, funciones escalares, literales de fecha y hora, literales de intervalo y combinaciones externas  
  
-   Bibliotecas de traducción de páginas de códigos  
  
-   Informes de nivel de conformidad con ANSI y la compatibilidad de SQL con un controlador  
  
-   Rellenado automático y a petición del descriptor de parámetro de implementación  
  
-   Diagnósticos mejorados y matrices de estado de fila y de parámetro  
  
-   Fecha y hora, intervalo, numérico o decimal y tipos de búfer de aplicación de entero de 64 bits  
  
-   Ejecución asincrónica  
  
-   Compatibilidad con los procedimientos almacenados, incluidas las secuencias de escape, mecanismos de enlace de parámetro de salida y funciones de catálogo  
  
-   Mejoras de conexión, incluida la compatibilidad con los atributos de conexión y la exploración de atributo
