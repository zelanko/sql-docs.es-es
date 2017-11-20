---
title: "Referencia de la API de archivo DLL de la instalación | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1bd84a225c94c4141cb9c7f6a897731926384ea6
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="setup-dll-api-reference"></a>Referencia de API de archivo DLL de instalación
Esta sección describe la sintaxis de la configuración de controladores de API de archivo DLL, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** puede estar en la DLL del controlador o en otro archivo DLL de la instalación.  
  
 Además, esta sección describe la sintaxis de la instalación de traductor API de DLL, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo DLL de traducción o en otro archivo DLL de la instalación.  
  
 Cada función tiene la etiqueta con la versión de ODBC en el que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [ConfigDriver (función)](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [ConfigDSN (función)](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [ConfigTranslator (función)](../../../odbc/reference/syntax/configtranslator-function.md)

