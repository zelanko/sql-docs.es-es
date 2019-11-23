---
title: Sys. syslanguages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.syslanguages
- sys.syslanguages_TSQL
- syslanguages
- syslanguages_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- syslanguages system table
- sys.syslanguages compatibility view
ms.assetid: f216d1cd-997c-42f0-a737-abbdfcd88383
author: rothja
ms.author: jroth
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bc152b8241b775f9fd686f8a31363cb4fca39de4
ms.sourcegitcommit: f76b4e96c03ce78d94520e898faa9170463fdf4f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/10/2019
ms.locfileid: "70874870"
---
# <a name="syssyslanguages-transact-sql"></a>sys.syslanguages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Contiene una fila por cada idioma presente en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|langid|**smallint**|Id. de idioma único.|  
|dateformat|**nchar(3)**|Orden de la fecha (por ejemplo, DMA).|  
|datefirst|**tinyint**|Primer día de la semana: 1 para lunes, 2 para martes y así sucesivamente hasta 7 para domingo.|  
|actualización|**int**|Reservado para uso del sistema.|  
|name|**sysname**|Nombre del idioma oficial, por ejemplo, Français.|  
|alias|**sysname**|Nombre alternativo del idioma (por ejemplo, francés).|  
|meses|**nvarchar(372)**|Lista separada por comas con los nombres completos de los meses, de enero a diciembre, en la que cada mes puede contener hasta 20 caracteres.|  
|shortmonths|**nvarchar(132)**|Lista separada por comas con los nombres cortos de los meses, de enero a diciembre, en la que cada mes puede contener hasta 9 caracteres.|  
|days|**nvarchar(217)**|Lista separada por comas con los nombres de los días, de lunes a domingo, en la que cada nombre puede contener hasta 30 caracteres.|  
|lcid|**int**|Id. de configuración regional de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows para el idioma.|  
|msglangid|**smallint**|Identificador del grupo de mensajes del [!INCLUDE[ssDE](../../includes/ssde-md.md)].|  
  
 El [!INCLUDE[ssDE](../../includes/ssde-md.md)] contiene los siguientes idiomas instalados.  
  
|Nombre en español|LCID de Windows|Id. de grupo de mensajes del [!INCLUDE[ssDE](../../includes/ssde-md.md)]|  
|---------------------|------------------|-----------------------------------------|  
|English|3082|3082|  
|German|1031|1031|  
|French|1036|1036|  
|Japanese|1041|1041|  
|Danés|1030|1030|  
|Spanish|3082|3082|  
|Italian|1040|1040|  
|Dutch|1043|1043|  
|Noruego|2068|2068|  
|Portugués|2070|2070|  
|Finlandés|1035|1035|  
|Swedish|1053|1053|  
|Czech|1029|1029|  
|Húngaro|1038|1038|  
|Polish|1045|1045|  
|Rumano|1048|1048|  
|Croatian|1050|1050|  
|Slovak|1051|1051|  
|Slovene|1060|1060|  
|Greek|1032|1032|  
|Bulgarian|1026|1026|  
|Russian|1049|1049|  
|Turkish|1055|1055|  
|British English|2057|3082|  
|Estonio|1061|1061|  
|Latvian|1062|1062|  
|Lithuanian|1063|1063|  
|Portuguese (Brazil)|1046|1046|  
|Traditional Chinese|1028|1028|  
|Korean|1042|1042|  
|Simplified Chinese|2052|2052|  
|Arabic|1025|1025|  
|Thai|1054|1054|  
  
## <a name="see-also"></a>Vea también  
 [Vistas &#40;de compatibilidad de Transact&#41; -SQL](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)   
 [Asignar tablas del sistema a las &#40;vistas del sistema TRANSACT-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)  
  
  
