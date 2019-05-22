---
title: 'Sys.external_languages (Transact-SQL): SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.reviewer: dphansen
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- external_languages
- external_languages_TSQL
- sys.external_languages
- sys.external_languages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.external_languages catalog view
author: nelgson
ms.author: negust
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 1cef52f066a07032240d17f88297b02ba3f7e5fb
ms.sourcegitcommit: be09f0f3708f2e8eb9f6f44e632162709b4daff6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65995123"
---
# <a name="sysexternallanguages-transact-sql"></a>sys.external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Esta vista de catálogo proporciona una lista de los idiomas en la base de datos externos. **R** y **Python** son nombres reservados y ningún idioma externo se puede crear con esos nombres específicos.

## <a name="sysexternallanguages"></a>sys.external_languages

El sys.external_languages de vista de catálogo contiene una fila para cada lenguaje externo en la base de datos.

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_language_id |INT | Identificador del idioma externo|
|language |sysname |Nombre del lenguaje externo. Es único en la base de datos. R y Python es nombres reservados por instancia|
|create_date |datetime2 |Fecha y hora de creación|
|principal_id |INT |Identificador de la entidad que posee esta biblioteca externa|

## <a name="see-also"></a>Vea también  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREACIÓN DE LENGUAJE EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md) 
