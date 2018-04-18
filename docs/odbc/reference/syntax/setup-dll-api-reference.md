---
title: Referencia de la API de archivo DLL de la instalación | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 33898a338fa93a9088065c116df4f1f46e873657
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="setup-dll-api-reference"></a>Referencia de API de archivo DLL de instalación
Esta sección describe la sintaxis de la configuración de controladores de API de archivo DLL, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** puede estar en la DLL del controlador o en otro archivo DLL de la instalación.  
  
 Además, esta sección describe la sintaxis de la instalación de traductor API de DLL, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo DLL de traducción o en otro archivo DLL de la instalación.  
  
 Cada función tiene la etiqueta con la versión de ODBC en el que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
