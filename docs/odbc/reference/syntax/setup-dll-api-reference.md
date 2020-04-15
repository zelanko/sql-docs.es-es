---
title: Referencia de la API de DLL de instalación ( DLL API Reference) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 25cff50b73868b5b3015dfc1a00c560c344a6d36
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298890"
---
# <a name="setup-dll-api-reference"></a>Referencia de API de DLL de instalación
En esta sección se describe la sintaxis de la API DLL de instalación del controlador, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** pueden estar en el archivo DLL del controlador o en un archivo DLL de instalación independiente.  
  
 Además, en esta sección se describe la sintaxis de la API DLL de instalación del traductor, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo DLL del traductor o en un archivo DLL de instalación independiente.  
  
 Cada función se etiqueta con la versión de ODBC en la que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
