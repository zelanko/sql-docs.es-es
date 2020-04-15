---
title: Tipos de Aplicaciones (En lo que se escapa de las aplicaciones) Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305536"
---
# <a name="types-of-applications"></a>Tipos de aplicaciones
Las aplicaciones ODBC se pueden clasificar de la siguiente manera:  
  
-   **ODBC 2 puro.**  
     ** _x_ Aplicación** Una aplicación de 32 bits que:  
  
    -   Solo llama ODBC 2. *x* funciones (incluida la función ODBC 1.0 **SQLSetParam**). Estos incluyen ODBC 1. *x* aplicaciones que se han portado a 32 bits.  
  
    -   Espera ODBC 2. *x* comportamiento para las entidades que han tenido cambios de comportamiento. (Consulte [Cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)  
  
    -   No se ha vuelto a compilar con encabezados ODBC 3.5.  
  
-   **ODBC 2 puro.**  
     **_x_ Aplicación recompilada** Un ODBC 2 puro. *x* aplicación que se ha vuelto a compilar mediante los archivos de encabezado ODBC 3.5, estableciendo ODBCVER-0x0250.  
  
-   **ODBC 2 puro.**  
     **_x_ Aplicación Unicode** Un ODBC 2 puro. *x* aplicación recompilada que es compatible con Unicode y utiliza el tipo de datos SQL_WCHAR.  
  
-   **Aplicación**-**ODBC compatible con** Pure Open Group y ISO Una aplicación de 32 bits que:  
  
    -   Llama a las funciones definidas en los estándares del grupo abierto o DE la CLI ISO. (Estas funciones pueden incluir funciones 3.0 en desuso.)  
  
    -   No utiliza los tipos de datos Unicode.  
  
    -   Espera un comportamiento ODBC 3.0 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3.0 pura** Una aplicación de 32 bits que:  
  
    -   Se compila con encabezados 3.0.  
  
    -   Llama a cualquier función ODBC 3.0, posiblemente incluidas las que están en desuso.  
  
    -   Espera un comportamiento ODBC 3.0 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3.5 pura** Una aplicación de 32 o 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función ODBC 3.5, posiblemente incluidas las que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.5 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación ODBC 3.8 (o posterior) pura** Una aplicación de 32 bits o 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función ODBC 3.8, posiblemente incluidas las que están en desuso.  
  
    -   Espera el comportamiento odbc 3.8 para las características que han tenido cambios de comportamiento.  
  
-   **Aplicación reemplazada** Una aplicación de 32 o 64 bits que:  
  
    -   Implementa un nuevo comportamiento para la funcionalidad duplicada.  
  
    -   Utiliza las nuevas características en una versión posterior de ODBC solo dentro del código condicional.  
  
    -   Tiene código condicional limitado para controlar los cambios de comportamiento o se ha registrado para ser una versión anterior de la aplicación ODBC.
