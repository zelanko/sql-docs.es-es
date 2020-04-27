---
title: Sys. external_language_files (Transact-SQL)-SQL Server | Microsoft Docs
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
ms.openlocfilehash: 0d1325311ef0b708f5a3abd5f4494e099863efc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "65995093"
---
# <a name="sysexternal_language_files-transact-sql"></a>Sys. external_language_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Esta vista de catálogo proporciona una lista de los archivos de extensión de lenguaje externo de la base de datos. **R** y **Python** son nombres reservados y no se puede crear ningún lenguaje externo con esos nombres.

Cuando se crea un lenguaje externo a partir de un file_spec, la propia extensión y sus propiedades se muestran en esta vista. Esta vista contendrá una entrada por idioma, por sistema operativo.

## <a name="sysexternal_languages"></a>sys.external_languages

La vista de catálogo sys. external_language_files muestra una fila para cada extensión de lenguaje externo de la base de datos. Parámetros

|Nombre de la columna |Tipo de datos | Descripción|
|------|------|------|
|external_language_id |int | IDENTIFICADOR del lenguaje externo|
|contenido|varbinary(max) |Contenido del archivo de extensión de lenguaje externo|
|file_name|nvarchar (266)|Nombre del archivo de extensión de idioma|
|platform|TINYINT|IDENTIFICADOR de la plataforma de host en la que está instalado SQL Server|
|platform_desc |nvarchar(60)|Nombre de la plataforma de host. Los valores válidos son ' WINDOWS ', ' LINUX '.|
|parámetros|nvarchar(4000)|Prameters de lenguaje externo|
|environment_variables |nvarchar(4000)|Variables de entorno de lenguaje externo|

## <a name="see-also"></a>Vea también  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CREAR LENGUAJE EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md)  
