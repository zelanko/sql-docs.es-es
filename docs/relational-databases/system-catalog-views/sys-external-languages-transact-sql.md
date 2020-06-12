---
title: Sys. external_languages (Transact-SQL)-SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
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
ms.reviewer: dphansen
manager: cgronlun
monikerRange: '>=sql-server-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 053a7cdcf21775525b0eb8d46bbbfdf03098e03c
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627280"
---
# <a name="sysexternal_languages-transact-sql"></a>Sys. external_languages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Esta vista de catálogo proporciona una lista de los idiomas externos en la base de datos. **R** y **Python** son nombres reservados y no se puede crear ningún lenguaje externo con esos nombres.

## <a name="sysexternal_languages"></a>sys.external_languages

La vista de catálogo sys. external_languages muestra una fila para cada lenguaje externo de la base de datos.

|Nombre de la columna |Tipo de datos | Descripción|
|------|------|------|
|external_language_id |int | IDENTIFICADOR del lenguaje externo|
|lenguaje |sysname |Nombre del idioma externo. Es único en la base de datos. R y Python son nombres reservados por instancia|
|create_date |datetime2 |Fecha y hora de creación|
|principal_id |int |IDENTIFICADOR de la entidad de seguridad que posee esta biblioteca externa|

## <a name="see-also"></a>Consulte también  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREAR LENGUAJE EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md) 
