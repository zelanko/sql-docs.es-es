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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 50e3e733a4ddd4855da2ea7722407e5f061eee47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63305724"
---
# <a name="types-of-applications"></a>Tipos de aplicaciones
Las aplicaciones ODBC pueden clasificarse como sigue:  
  
-   **Puro ODBC 2.**  
     **_x_ aplicación** aplicación de 32 bits que:  
  
    -   Llama a sólo ODBC 2. *x* funciones (incluida la función ODBC 1.0 **SQLSetParam**). Estos incluyen el 1 de ODBC. *x* las aplicaciones que se han trasladado a 32 bits.  
  
    -   Espera a que ODBC 2. *x* comportamiento para aquellas características que han tenido los cambios de comportamiento. (Consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)  
  
    -   No se han recopilado con encabezados de ODBC 3.5.  
  
-   **Puro ODBC 2.**  
     **_x_ vuelve a compilar la aplicación** una pura ODBC 2. *x* aplicación que se ha vuelto a compilar con los archivos de encabezado ODBC 3.5, estableciendo ODBCVER = 0x0250.  
  
-   **Puro ODBC 2.**  
     **_x_ aplicación Unicode** una pura ODBC 2. *x* vuelve a compilar la aplicación que es compatible con Unicode y utiliza el tipo de datos SQL_WCHAR.  
  
-   **Open Group puras e ISO**-**compatible con aplicaciones ODBC** aplicación de 32 bits que:  
  
    -   Llama a las funciones definidas en los estándares de Open Group o ISO CLI. (Estas funciones pueden incluir 3.0 funciones en desuso).  
  
    -   No utiliza los tipos de datos Unicode.  
  
    -   Espera el comportamiento de ODBC 3.0 para aquellas características que han tenido los cambios de comportamiento.  
  
-   **Aplicación pura ODBC 3.0** aplicación de 32 bits que:  
  
    -   Se compila con 3.0 encabezados.  
  
    -   Llama a cualquier función ODBC 3.0, posiblemente, incluidas las que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.0 para aquellas características que han tenido los cambios de comportamiento.  
  
-   **Aplicación pura ODBC 3.5** A 32 o aplicación de 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función ODBC 3.5, posiblemente, incluidas las que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.5 para aquellas características que han tenido los cambios de comportamiento.  
  
-   **Aplicación pura de 3,8 (o posterior) de ODBC** aplicación de 32 bits o 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función ODBC 3.8, posiblemente, incluidas las que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.8 para aquellas características que han tenido los cambios de comportamiento.  
  
-   **Reemplazar aplicación** A 32 o aplicación de 64 bits que:  
  
    -   Implementa el comportamiento nuevo para la funcionalidad de duplicados.  
  
    -   Usa las nuevas características en una versión posterior de ODBC solo dentro de código condicional.  
  
    -   Tiene limitado el código condicional para controlar los cambios de comportamiento o se ha registrado para que sea una versión anterior de la aplicación de ODBC.
