---
title: Tipos de aplicaciones | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading applications [ODBC], application types
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
- application upgrades [ODBC], application types
- application compatibility issues [ODBC]
ms.assetid: d346a64e-a32c-4153-a40f-5b53c2f57ef2
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 26835fa277391f359d628ec25c03d38364e398e7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="types-of-applications"></a>Tipos de aplicaciones
Las aplicaciones ODBC pueden clasificarse de la siguiente manera:  
  
-   **Puro ODBC 2.**  
     ***x* aplicación** aplicación de 32 bits que:  
  
    -   Llama a solo ODBC 2. *x* funciones (incluida la función de ODBC 1.0 **SQLSetParam**). Se trata de 1 de ODBC. *x* las aplicaciones que se han trasladado a 32 bits.  
  
    -   Espera que ODBC 2. *x* comportamiento para aquellas características que han tenido cambios de comportamiento. (Consulte [cambios de comportamiento](../../../odbc/reference/develop-app/behavioral-changes.md) para obtener más información.)  
  
    -   No se han recopilado con encabezados de ODBC 3.5.  
  
-   **Puro ODBC 2.**  
     ***x* vuelve a compilar la aplicación** un puro ODBC 2.* x* aplicación que se ha vuelto a compilar utilizando los archivos de encabezado ODBC 3.5, estableciendo ODBCVER = 0x0250.  
  
-   **Puro ODBC 2.**  
     ***x* aplicación Unicode** un puro ODBC 2.* x* vuelve a compilar la aplicación que es compatible con Unicode y usa el tipo de datos SQL_WCHAR.  
  
-   **Open Group puras e ISO**:**aplicaciones ODBC compatibles con** aplicación de 32 bits que:  
  
    -   Llama a las funciones definidas en las normas ISO CLI o de Open Group. (Estas funciones pueden incluir 3.0 funciones en desuso).  
  
    -   No utiliza los tipos de datos Unicode.  
  
    -   Espera el comportamiento de ODBC 3.0 para aquellas características que han tenido cambios de comportamiento.  
  
-   **Aplicación pura ODBC 3.0** aplicación de 32 bits que:  
  
    -   Se compila con 3.0 encabezados.  
  
    -   Llama a cualquier función de ODBC 3.0, posiblemente, incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.0 para aquellas características que han tenido cambios de comportamiento.  
  
-   **Aplicación pura ODBC 3.5** A 32 o una aplicación de 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función de ODBC 3.5, posiblemente, incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.5 para aquellas características que han tenido cambios de comportamiento.  
  
-   **Aplicación pura de 3.8 (o posterior) de ODBC** aplicación de 32 bits o 64 bits que:  
  
    -   Puede usar tipos de datos Unicode.  
  
    -   Llama a cualquier función de ODBC 3.8, posiblemente, incluidos los que están en desuso.  
  
    -   Espera el comportamiento de ODBC 3.8 para aquellas características que han tenido cambios de comportamiento.  
  
-   **Reemplazar aplicaciones** A 32 o una aplicación de 64 bits que:  
  
    -   Implementa el comportamiento nuevo para la funcionalidad de duplicados.  
  
    -   Usa las nuevas características en una versión posterior de ODBC solo dentro de código condicional.  
  
    -   Tiene limitado el código condicional para controlar los cambios de comportamiento o se ha registrado para que sea una versión anterior de la aplicación de ODBC.

