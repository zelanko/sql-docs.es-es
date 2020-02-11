---
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 7d26f2d33d81e08cfe4bddff9b2260bd2f098f00
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68093942"
---
# <a name="odbc-translators-subkey"></a>Subclave de traductores de ODBC
Los valores de la subclave traductores ODBC enumeran los traductores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*Traductor: DESC*|REG_SZ|**Instalación**|  
  
 El desarrollador de traductor define el nombre *de Translator-DESC* .  
  
 Por ejemplo, supongamos que un usuario ha instalado Microsoft® traductor de páginas de códigos y un traductor de ASCII a EBCDIC personalizado. Los valores de la subclave traductores ODBC pueden ser los siguientes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
