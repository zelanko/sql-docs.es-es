---
description: Referencia de API de DLL de instalación
title: Referencia de API de DLL de configuración | Microsoft Docs
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
ms.openlocfilehash: 5cb3e20a1c25d206a1dd27367bbe4a128af0818f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88487338"
---
# <a name="setup-dll-api-reference"></a>Referencia de API de DLL de instalación
En esta sección se describe la sintaxis de la API de DLL de instalación del controlador, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** pueden estar en el archivo DLL del controlador o en un archivo dll de instalación independiente.  
  
 Además, en esta sección se describe la sintaxis de la API de DLL de instalación de Translator, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo dll de traductor o en un archivo dll de instalación independiente.  
  
 Cada función tiene la etiqueta de la versión de ODBC en la que se presentó.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
