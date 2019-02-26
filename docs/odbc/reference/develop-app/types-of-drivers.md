---
title: Tipos de controladores | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 445fe3a0b87e6ad8e35dbc585981d874f8e357bf
ms.sourcegitcommit: bfa10c54e871700de285d7f819095d51ef70d997
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/14/2019
ms.locfileid: "54256960"
---
# <a name="types-of-drivers"></a>Tipos de controladores
Controladores ODBC se pueden clasificar como sigue:  
  
-   **2 de ODBC de 32 bits.**  
     **_x_ controlador** controladores de 32 bits que:  
  
    -   Exporta solo ODBC 2 *.x* funciones.  
  
    -   Exhibe ODBC 2.*x* comportamiento cambios de comportamiento.  
  
-   **ISO y el controlador de grupo conforme abra** controladores de 32 bits que:  
  
    -   Exporta todas las funciones que se documentan en los documentos de Open Group o ISO CLI. Esto incluye algunas de las funciones que están en desuso en ODBC.  
  
    -   Exhibe un comportamiento de ODBC 3.0 para cambios de comportamiento.  
  
    -   No necesariamente pasa a través del Administrador de controladores ODBC 3.0.  
  
-   **Controladores ODBC 3.0** controladores de 32 bits que:  
  
    -   Exporta solo las funciones que se encuentran en ODBC 3.0 menos funciones en desuso.  
  
    -   Es capaz de presenta ODBC 2.*x* comportamiento o el comportamiento de ODBC 3.0 con respecto a los cambios de comportamiento, según el atributo de entorno SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Controlador ODBC 3.5 (o posterior) ANSI** controladores de 32 bits que:  
  
    -   Exporta solo las funciones que se encuentran en ODBC 3.5 menos funciones en desuso.  
  
    -   Es capaz de presenta ODBC 2. *x* comportamiento o el comportamiento de ODBC 3.0 o el comportamiento de ODBC 3.5 con respecto a los cambios de comportamiento, según el atributo de entorno SQL_ATTR_APP_ODBC_VERSION.  
  
-   **Controlador ODBC 3.5 (o posterior) Unicode** controladores de 32 bits que:  
  
    -   Es compatible con todas las características de un controlador de ODBC 3.5 ANSI.  
  
    -   Exporta las versiones Unicode de todas las API de cadena de ODBC.  
  
    -   Puede almacenar y procesar los datos Unicode en el origen de datos.  
  
> [!NOTE]  
>  controladores ODBC de 16 bits no funcionará directamente con ODBC 3. *x* Administrador de controladores. Sin embargo, es posible que los controladores de 16 bits trabajar con el Administrador de controladores ODBC 2.0, que posteriormente thunks hasta el 3. *x* Administrador de controladores.
