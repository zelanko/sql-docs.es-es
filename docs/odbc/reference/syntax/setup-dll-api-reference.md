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
manager: craigg
ms.openlocfilehash: d81bb9f5ec54f3d66089205f5b5941119d365501
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62652903"
---
# <a name="setup-dll-api-reference"></a>Referencia de API de DLL de instalación
En esta sección se describe la sintaxis de la configuración del controlador de API de DLL, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** puede estar en la DLL del controlador o en otro archivo DLL de configuración.  
  
 Además, esta sección describe la sintaxis de la configuración de translator API de DLL, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo DLL de traducción o en otro archivo DLL de configuración.  
  
 Cada función se etiqueta con la versión de ODBC en el que se introdujo.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
