---
title: Tipos de aplicaciones | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f14326c9cec1eb89e431154c91b680e4688fcdfa
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81305536"
---
# <a name="types-of-applications"></a>Tipos de aplicaciones
Las aplicaciones ODBC se pueden clasificar de la siguiente manera:  
  
-   **ODBC 2 puro.**  
     **aplicación _x_ ** una aplicación de 32 bits que:  
  
    -   Solo llama a ODBC 2. funciones *x* (incluida la función **SQLSetParam**de ODBC 1,0). Estos incluyen ODBC 1. aplicaciones *x* que se han trasladado a 32 bits.  
  
    -   Espera ODBC 2. comportamiento de *x* para las características que han tenido cambios de comportamiento. (Vea [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información).  
  
    -   No se ha vuelto a compilar con encabezados ODBC 3,5.  
  
-   **ODBC 2 puro.**  
     **_x_ aplicación recompilada** : ODBC 2 puro. aplicación *x* que se ha vuelto a compilar mediante los archivos de encabezado ODBC 3,5, estableciendo ODBCVER = 0x0250.  
  
-   **ODBC 2 puro.**  
     **la aplicación Unicode _x_ ** es un ODBC 2 puro. *x* aplicación recompilada que es compatible con Unicode y usa el tipo de datos SQL_WCHAR.  
  
-   **Aplicación ODBC pura de grupo abierto e ISO**-**con** una aplicación de 32 bits que:  
  
    -   Llama a las funciones definidas en los estándares Open Group o ISO CLI. (Estas funciones pueden incluir funciones 3,0 desusadas).  
  
    -   No utiliza los tipos de datos Unicode.  
  
    -   Espera el comportamiento de ODBC 3,0 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3,0 pura** Una aplicación de 32 bits que:  
  
    -   Se compila con encabezados 3,0.  
  
    -   Llama a cualquier función de ODBC 3,0, posiblemente incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3,0 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3,5 pura** Una aplicación de 32 o 64 bits que:  
  
    -   Puede utilizar tipos de datos Unicode.  
  
    -   Llama a cualquier función de ODBC 3,5, posiblemente incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3,5 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3,8 (o posterior) pura** Una aplicación de 32 bits o de 64 bits que:  
  
    -   Puede utilizar tipos de datos Unicode.  
  
    -   Llama a cualquier función de ODBC 3,8, posiblemente incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3,8 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación reemplazada** Una aplicación de 32 o 64 bits que:  
  
    -   Implementa un nuevo comportamiento para la funcionalidad duplicada.  
  
    -   Usa todas las características nuevas de una versión posterior de ODBC únicamente en el código condicional.  
  
    -   Tiene código condicional limitado para controlar los cambios de comportamiento o se ha registrado para ser una versión anterior de la aplicación ODBC.
