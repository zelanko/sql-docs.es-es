---
description: Subclave de traductores de ODBC
title: Subclave de traductores ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- translator subkey [ODBC]
- subkeys [ODBC], translator subkey
- registry entries for components [ODBC], translator subkey
ms.assetid: 6b170f1f-e263-4aac-9d49-8d0ca0470ca2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 46308518f1f806cea21bbb824312d5269f8b61e4
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499718"
---
# <a name="odbc-translators-subkey"></a>Subclave de traductores de ODBC
Los valores de la subclave traductores ODBC enumeran los traductores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*Traductor: DESC*|REG_SZ|**Instalado**|  
  
 El desarrollador de traductor define el nombre *de Translator-DESC* .  
  
 Por ejemplo, supongamos que un usuario ha instalado Microsoft® traductor de páginas de códigos y un traductor de ASCII a EBCDIC personalizado. Los valores de la subclave traductores ODBC pueden ser los siguientes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
