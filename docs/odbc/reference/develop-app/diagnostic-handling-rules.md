---
title: Diagnóstico de las reglas de control | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9f59953dee77453bb8b453a40a36d17e865a1fe5
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63034932"
---
# <a name="diagnostic-handling-rules"></a>Reglas de control de diagnóstico
Las reglas siguientes rigen el control de diagnóstico en **SQLGetDiagRec** y **SQLGetDiagField**.  
  
 Para todos los componentes ODBC:  
  
-   Debe no reemplazar, modificar o enmascarar errores o advertencias recibidas de otro componente ODBC.  
  
-   Puede agregar un registro de estado adicionales al recibir un mensaje de diagnóstico de otro componente ODBC. El registro se ha agregado debe agregar el valor de la información real al mensaje original.  
  
 Para ODBC componente interfaces directamente de un origen de datos:  
  
-   Debe anteponer el identificador del origen de datos para el mensaje de diagnóstico que recibe desde el origen de datos, su identificador de componente y su identificador de proveedor.  
  
-   Debe conservar el código de error nativo del origen de datos.  
  
-   Debe conservar el mensaje de diagnóstico del origen de datos.  
  
 Para cualquier componente ODBC que genera un error o advertencia independiente del origen de datos:  
  
-   Debe proporcionar el valor de SQLSTATE correcto para el error o advertencia.  
  
-   Debe generar el texto del mensaje de diagnóstico.  
  
-   Debe agregar un prefijo su identificador de proveedor y su identificador de componente para el mensaje de diagnóstico.  
  
-   Debe devolver un código de error nativo, si está disponible y significativas.  
  
 Para el componente ODBC que interactúa con el Administrador de controladores:  
  
-   Debe inicializar los argumentos de salida **SQLGetDiagRec** y **SQLGetDiagField**.  
  
-   Debe dar formato y devolver la información de diagnóstico como argumentos de salida **SQLGetDiagRec** y **SQLGetDiagField** cuando se llama a esa función.  
  
 Para un componente ODBC que no sea el Administrador de controladores:  
  
-   Debe establecer el valor de SQLSTATE según el error nativo. Para obtener controladores basados en archivos y controladores basados en DBMS que no usan una puerta de enlace, el controlador debe establecer el valor de SQLSTATE. Para los controladores basados en DBMS que usar una puerta de enlace, el controlador o una puerta de enlace que admite ODBC puede establecer el valor de SQLSTATE.
