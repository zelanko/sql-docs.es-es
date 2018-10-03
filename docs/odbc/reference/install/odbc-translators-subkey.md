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
manager: craigg
ms.openlocfilehash: 9e7109a6f1b88cf7639b2fc823ce0c5f14d05002
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47673243"
---
# <a name="odbc-translators-subkey"></a>Subclave de traductores de ODBC
Los valores bajo la subclave de traductores de ODBC enumeran los traductores instalados. En la tabla siguiente se muestra el formato de estos valores.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*traductor desc*|REG_SZ|**instalado**|  
  
 El *traductor desc* nombre se define mediante el programador de traductor.  
  
 Por ejemplo, suponga que un usuario ha instalado el traductor de páginas de código de Microsoft® y un ASCII personalizado al traductor de EBCDIC. Los valores bajo la subclave de traductores de ODBC podrían ser como sigue:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
