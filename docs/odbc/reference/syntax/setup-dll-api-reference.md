---
title: Referencia de API de DLL de instalación | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC drivers [ODBC], driver setup DLL
- driver setup DLL [ODBC]
ms.assetid: f9d03f17-1c0d-4e7c-9c04-8c316e07ef25
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 26e5c36b41f68627a634714cfa06525c99451450
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67947052"
---
# <a name="setup-dll-api-reference"></a>Referencia de API de DLL de instalación
En esta sección se describe la sintaxis de la configuración del controlador de API de DLL, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** puede estar en la DLL del controlador o en otro archivo DLL de configuración.  
  
 Además, esta sección describe la sintaxis de la configuración de translator API de DLL, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo DLL de traducción o en otro archivo DLL de configuración.  
  
 Cada función se etiqueta con la versión de ODBC en el que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
