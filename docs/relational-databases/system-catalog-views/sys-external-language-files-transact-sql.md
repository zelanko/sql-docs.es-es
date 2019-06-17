---
title: 'Sys.external_language_files (Transact-SQL): SQL Server | Microsoft Docs'
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65995093"
---
# <a name="sysexternallanguagefiles-transact-sql"></a>sys.external_language_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ssver15-xxxx-xxxx-xxx](../../includes/tsql-appliesto-ssver15-xxxx-xxxx-xxx.md)]

Esta vista de catálogo proporciona una lista de los archivos de extensión de lenguaje externo en la base de datos. **R** y **Python** son nombres reservados y no se puede crear ningún lenguaje externo con esos nombres.

Cuando se crea un lenguaje externo desde una file_spec, la propia extensión y sus propiedades se enumeran en esta vista. Esta vista contiene una entrada por cada idioma, por el sistema operativo.

## <a name="sysexternallanguages"></a>sys.external_languages

El sys.external_language_files de vista de catálogo contiene una fila para cada extensión de lenguaje externo en la base de datos. Parámetros

|Nombre de columna |Tipo de datos | Descripción|
|------|------|------|
|external_language_id |INT | Identificador del idioma externo|
|content|varbinary(max) |Contenido del archivo de extensión de lenguaje externo|
|file_name|nvarchar(266)|Nombre del archivo de extensión de lenguaje|
|Plataforma|TINYINT|Id. de la plataforma de host donde está instalado SQL Server|
|platform_desc |nvarchar(60)|Nombre de la plataforma de host. Los valores válidos son 'WINDOWS', 'LINUX'.|
|Parámetros|nvarchar(4000)|Lenguaje externo prameters|
|environment_variables |nvarchar(4000)|Variables de entorno de lenguaje externo|

## <a name="see-also"></a>Vea también  

+ [sys.external_languages](sys-external-languages-transact-sql.md)  
+ [CREACIÓN DE LENGUAJE EXTERNO](../../t-sql/statements/create-external-language-transact-sql.md)  
