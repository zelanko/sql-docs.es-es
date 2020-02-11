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
ms.openlocfilehash: ea99ec6a5b0a76ce0647e3681a4cf919d3f086b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087775"
---
# <a name="types-of-drivers"></a>Tipos de controladores
Los controladores ODBC se pueden clasificar de la siguiente manera:  
  
-   **ODBC 2 de 32 bits.**  
     controlador ** _x_ ** un controlador de 32 bits que:  
  
    -   Exporta solo funciones ODBC *2. x* .  
  
    -   Exhibe el comportamiento de ODBC *2. x* para los cambios de comportamiento.  
  
-   **ISO y abrir controlador compatible con grupos** Un controlador de 32 bits que:  
  
    -   Exporta todas las funciones que se documentan en los documentos Open Group o CLI ISO. Esto incluirá algunas de las funciones que están desusadas en ODBC.  
  
    -   Exhibe el comportamiento de ODBC 3,0 para los cambios de comportamiento.  
  
    -   No pasa necesariamente por el administrador de controladores ODBC 3,0.  
  
-   **Controlador ODBC 3,0** Un controlador de 32 bits que:  
  
    -   Exporta solo las funciones que se encuentran en ODBC 3,0 menos funciones desusadas.  
  
    -   Es capaz de presentar el comportamiento de ODBC *2. x* o el comportamiento de ODBC 3,0 con respecto a los cambios de comportamiento, según el atributo de entorno de SQL_ATTR_APP_ODBC_VERSION.  
  
-   **ODBC 3,5 (o posterior) controlador ANSI** Un controlador de 32 bits que:  
  
    -   Exporta solo las funciones que se encuentran en ODBC 3,5 menos funciones desusadas.  
  
    -   Es capaz de presentar el comportamiento de ODBC *2. x* o el comportamiento de ODBC 3,0, o el comportamiento de ODBC 3,5 con respecto a los cambios de comportamiento, según el atributo de entorno de SQL_ATTR_APP_ODBC_VERSION.  
  
-   **ODBC 3,5 (o posterior) controlador Unicode** Un controlador de 32 bits que:  
  
    -   Admite todas las características de un controlador ODBC 3,5 ANSI.  
  
    -   Exporta versiones Unicode de todas las API de cadena ODBC.  
  
    -   Puede almacenar y procesar datos Unicode en el origen de datos.  
  
> [!NOTE]  
>  los controladores ODBC de 16 bits no funcionarán directamente con el administrador de controladores ODBC *3. x* . Sin embargo, es posible que los controladores de 16 bits funcionen con el administrador de controladores ODBC 2,0, que posteriormente se thunks hasta el administrador de controladores *3. x* .
