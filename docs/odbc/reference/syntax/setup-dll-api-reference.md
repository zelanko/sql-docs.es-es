---
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
ms.openlocfilehash: 25cff50b73868b5b3015dfc1a00c560c344a6d36
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81298890"
---
# <a name="setup-dll-api-reference"></a>Referencia de API de DLL de instalación
En esta sección se describe la sintaxis de la API de DLL de instalación del controlador, que consta de dos funciones (**ConfigDriver** y **ConfigDSN**). **ConfigDriver** y **ConfigDSN** pueden estar en el archivo DLL del controlador o en un archivo dll de instalación independiente.  
  
 Además, en esta sección se describe la sintaxis de la API de DLL de instalación de Translator, que consta de una sola función (**ConfigTranslator**). **ConfigTranslator** puede estar en el archivo dll de traductor o en un archivo dll de instalación independiente.  
  
 Cada función tiene la etiqueta de la versión de ODBC en la que se presentó.  
  
 Esta sección contiene los temas siguientes.  
  
-   [Función ConfigDriver](../../../odbc/reference/syntax/configdriver-function.md)  
  
-   [Función ConfigDSN](../../../odbc/reference/syntax/configdsn-function.md)  
  
-   [Función ConfigTranslator](../../../odbc/reference/syntax/configtranslator-function.md)
