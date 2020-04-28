---
title: Reglas de control de diagnóstico | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], SqlGetDiagField
- SQLGetDiagField function [ODBC], diagnostic handling rules
- SQLGetDiagRec function [ODBC], diagnostic handling rules
- diagnostic information [ODBC], SqlGetDiagRec
ms.assetid: 74387c3a-d6b3-4c35-b209-b9612602b20a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9f7f9d19a5a369e9da0efbc0d62f8e556b0597c1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305846"
---
# <a name="diagnostic-handling-rules"></a>Reglas de control de diagnóstico
Las siguientes reglas rigen el control de diagnóstico en **SQLGetDiagRec** y **SQLGetDiagField**.  
  
 Para todos los componentes ODBC:  
  
-   No debe reemplazar, modificar ni enmascarar los errores o las advertencias recibidas de otro componente ODBC.  
  
-   Puede Agregar un registro de estado adicional cuando reciba un mensaje de diagnóstico de otro componente ODBC. El registro agregado debe agregar el valor real de la información al mensaje original.  
  
 Para el componente ODBC que interactúa directamente con un origen de datos:  
  
-   Debe anteponer su identificador de proveedor, su identificador de componente y el identificador del origen de datos al mensaje de diagnóstico que recibe del origen de datos.  
  
-   Debe conservar el código de error nativo del origen de datos.  
  
-   Debe conservar el mensaje de diagnóstico del origen de datos.  
  
 Para cualquier componente ODBC que genere un error o una advertencia independientemente del origen de datos:  
  
-   Debe proporcionar el SQLSTATE correcto para el error o la advertencia.  
  
-   Debe generar el texto del mensaje de diagnóstico.  
  
-   Debe anteponer su identificador de proveedor y su identificador de componente al mensaje de diagnóstico.  
  
-   Debe devolver un código de error nativo, si hay alguno disponible y significativo.  
  
 Para el componente ODBC que interactúa con el administrador de controladores:  
  
-   Debe inicializar los argumentos de salida de **SQLGetDiagRec** y **SQLGetDiagField**.  
  
-   Debe dar formato y devolver la información de diagnóstico como argumentos de salida de **SQLGetDiagRec** y **SQLGetDiagField** cuando se llama a esa función.  
  
 Para un componente ODBC que no sea el administrador de controladores:  
  
-   Debe establecer el valor de SQLSTATE en función del error nativo. En el caso de los controladores basados en archivos y los controladores basados en DBMS que no usan una puerta de enlace, el controlador debe establecer SQLSTATE. En el caso de los controladores basados en DBMS que usan una puerta de enlace, es posible que el controlador o una puerta de enlace compatibles con ODBC establezcan el SQLSTATE.
