---
title: Reglas de Manejo de Diagnóstico (Diagnóstico de las Reglas de Manejo de Diagnóstico Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305846"
---
# <a name="diagnostic-handling-rules"></a>Reglas de control de diagnóstico
Las reglas siguientes rigen el control de diagnóstico en **SQLGetDiagRec** y **SQLGetDiagField**.  
  
 Para todos los componentes ODBC:  
  
-   No debe reemplazar, alterar o enmascarar errores o advertencias recibidas de otro componente ODBC.  
  
-   Puede agregar un registro de estado adicional cuando reciban un mensaje de diagnóstico de otro componente ODBC. El registro agregado debe agregar valor de información real al mensaje original.  
  
 Para el componente ODBC que interconecta directamente un origen de datos:  
  
-   Debe prefijar su identificador de proveedor, su identificador de componente y el identificador del origen de datos en el mensaje de diagnóstico que recibe del origen de datos.  
  
-   Debe conservar el código de error nativo del origen de datos.  
  
-   Debe conservar el mensaje de diagnóstico del origen de datos.  
  
 Para cualquier componente ODBC que genere un error o advertencia independientedel del origen de datos:  
  
-   Debe proporcionar el SQLSTATE correcto para el error o la advertencia.  
  
-   Debe generar el texto del mensaje de diagnóstico.  
  
-   Debe prefijar su identificador de proveedor y su identificador de componente al mensaje de diagnóstico.  
  
-   Debe devolver un código de error nativo, si uno está disponible y es significativo.  
  
 Para el componente ODBC que interactúa con el Administrador de controladores:  
  
-   Debe inicializar los argumentos de salida de **SQLGetDiagRec** y **SQLGetDiagField**.  
  
-   Debe dar formato y devolver la información de diagnóstico como argumentos de salida de **SQLGetDiagRec** y **SQLGetDiagField** cuando se llama a esa función.  
  
 Para un componente ODBC distinto del Administrador de controladores:  
  
-   Debe establecer SQLSTATE en función del error nativo. Para los controladores basados en archivos y los controladores basados en DBMS que no utilizan una puerta de enlace, el controlador debe establecer SQLSTATE. Para los controladores basados en DBMS que utilizan una puerta de enlace, el controlador o una puerta de enlace que admite ODBC puede establecer SQLSTATE.
