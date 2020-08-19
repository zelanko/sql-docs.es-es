---
description: Sys. external_languages (Transact-SQL)-SQL Server
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
ms.openlocfilehash: 1f44ce24baf72b5bb93e8d649d8fa4ebed1d6e99
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88420129"
---
# <a name="sysexternal_languages-transact-sql"></a>Sys. external_languages (Transact-SQL)
[!INCLUDE[SQL Server 2019](../../includes/applies-to-version/sqlserver2019.md)]

Esta vista de catálogo proporciona una lista de los idiomas externos en la base de datos. **R** y **Python** son nombres reservados y no se puede crear ningún lenguaje externo con esos nombres.

## <a name="sysexternal_languages"></a>sys.external_languages

La vista de catálogo sys. external_languages muestra una fila para cada lenguaje externo de la base de datos.

|Nombre de la columna |Tipo de datos | Descripción|
|------|------|------|
|external_language_id |int | IDENTIFICADOR del lenguaje externo|
|language |sysname |Nombre del idioma externo. Es único en la base de datos. R y Python son nombres reservados por instancia|
|create_date |datetime2 |Fecha y hora de creación|
|principal_id |int |IDENTIFICADOR de la entidad de seguridad que posee esta biblioteca externa|

## <a name="see-also"></a>Consulte también  

+ [sys.external_language_files](sys-external-language-files-transact-sql.md)  
+ [CREAR LENGUAJE EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md) 
