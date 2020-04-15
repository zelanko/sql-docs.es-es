---
title: Tipos de Conductores (Tipos de Conductores) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- driver compatibility issues [ODBC]
- ODBC drivers [ODBC], backward compatibility
- backward compatibility [ODBC], application and driver compatibility
- compatibility [ODBC], application and driver compatibility
ms.assetid: 864c53c1-b68a-48b6-b6bc-5ecb520bb9dc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: de6d8e1473f127d28c69969e0fc298afd69d3023
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304876"
---
# <a name="types-of-drivers"></a>Tipos de controladores
Los controladores ODBC se pueden clasificar de la siguiente manera:  
  
-   **ODBC 2 de 32 bits.**  
     ** _x_ Controlador** Un controlador de 32 bits que:  
  
    -   Exporta solo funciones ODBC *2.x.*  
  
    -   Muestra el comportamiento de ODBC *2.x* para los cambios de comportamiento.  
  
-   **Controlador compatible con isO y grupo abierto** Un controlador de 32 bits que:  
  
    -   Exporta todas las funciones que se documentan en los documentos de Open Group o ISO CLI. Esto incluirá algunas de las funciones que están en desuso en ODBC.  
  
    -   Muestra el comportamiento de ODBC 3.0 para los cambios de comportamiento.  
  
    -   No necesariamente pasa por el Administrador de controladores ODBC 3.0.  
  
-   **Controlador ODBC 3.0** Un controlador de 32 bits que:  
  
    -   Exporta solo las funciones que están en ODBC 3.0 menos funciones en desuso.  
  
    -   Es capaz de mostrar el comportamiento ODBC *2.x* o el comportamiento de ODBC 3.0 con respecto a los cambios de comportamiento, en función del atributo de entorno SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Controlador ANSI ODBC 3.5 (o posterior)** Un controlador de 32 bits que:  
  
    -   Exporta solo las funciones que están en ODBC 3.5 menos funciones en desuso.  
  
    -   Es capaz de mostrar el comportamiento ODBC *2.x* o el comportamiento ODBC 3.0, o el comportamiento de ODBC 3.5 con respecto a los cambios de comportamiento, en función del atributo de entorno SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Controlador Unicode ODBC 3.5 (o posterior)** Un controlador de 32 bits que:  
  
    -   Admite todas las características de un controlador ODBC 3.5 ANSI.  
  
    -   Exporta versiones Unicode de todas las API de cadena ODBC.  
  
    -   Puede almacenar y procesar datos Unicode en el origen de datos.  
  
> [!NOTE]  
>  Los controladores ODBC de 16 bits no funcionarán directamente con el Administrador de controladores ODBC *3.x.* Sin embargo, es posible que los controladores de 16 bits funcionen con el Administrador de controladores ODBC 2.0, que posteriormente se thunks hasta el Administrador de controladores *3.x.*
