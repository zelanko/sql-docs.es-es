---
title: Subclave de traductores ODBC (ODBC Translators Subkey) Microsoft Docs
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
ms.openlocfilehash: 617416adfcddfbf041c48acbf83cb9589e34ae27
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81296225"
---
# <a name="odbc-translators-subkey"></a>Subclave de traductores de ODBC
Los valores de la subclave TRADUCTORes ODBC enumeran los traductores instalados. El formato de estos valores se muestra en la tabla siguiente.  
  
|Nombre|Tipo de datos|data|  
|----------|---------------|----------|  
|*traductor-desc*|REG_SZ|**Instalado**|  
  
 El nombre *translator-desc* lo define el desarrollador del traductor.  
  
 Por ejemplo, supongamos que un usuario ha instalado Microsoft® Code Page Translator y un traductor personalizado de ASCII a EBCDIC. Los valores de la subclave Traductores ODBC pueden ser los siguientes:  
  
```  
MS Code Page Translator: REG_SZ : Installed  
ASCII to EBCDIC: REG_SZ : Installed.  
```
