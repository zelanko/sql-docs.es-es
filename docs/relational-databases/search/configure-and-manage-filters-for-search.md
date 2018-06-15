---
title: Configurar y administrar filtros para búsquedas | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.component: search
ms.reviewer: ''
ms.suite: sql
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: d5581011c38ace01ab61acf62c1d084893d8b9de
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
ms.locfileid: "33178381"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurar y administrar filtros para búsquedas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La indexación de documentos en una columna de tipo de datos **varbinary**, **varbinary(max)**, **image**, o **xml** exige un procesamiento adicional. Un filtro debe realizar este procesamiento. El filtro extrae la información de texto del documento y quita el formato. A continuación, el filtro envía el texto al componente separador de palabras correspondiente al idioma asociado a la columna de la tabla.  
 
## <a name="filters-and-document-types"></a>Tipos de documento y filtro
Un filtro determinado es específico de un tipo de documento concreto (.doc, .pdf, .xls, .xml, etc.). Estos filtros implementan la interfaz IFilter. Para obtener más información de estos tipos de documento, consulte la vista de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
Los documentos binarios se pueden almacenar en una sola columna de tipo **varbinary(max)** o **image** . Para cada documento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elige el filtro correcto de acuerdo con la extensión de archivo. Dado que la extensión de archivo no está visible cuando el archivo se almacena en una columna de tipo **varbinary(max)** o **image** , la extensión de archivo (.doc, .xls, .pdf, etcétera) debe almacenarse en una columna independiente de la tabla, denominada columna de tipo. Esta columna de tipo debe ser de cualquier tipo de datos basado en caracteres y debe contener la extensión del archivo, como .doc para los documentos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. En la tabla **Document** en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], la columna **Document** es de tipo **varbinary(max)** y la columna de tipo **FileExtension**es de tipo **nvarchar(8)**.  

**Para ver la columna de tipo en un índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  Un filtro podría ser capaz de tratar los incrustados en el objeto primario, dependiendo de su implementación. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no configura los filtros para seguir los vínculos a otros objetos.  

## <a name="installed-filters"></a>Filtros instalados 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala sus propios filtros HTML y XML. Además, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también carga los filtros para formatos de propietario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (.doc, .xdoc, .ppt, etcétera) que ya están instalados en el sistema operativo. Para identificar los filtros que están cargados actualmente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , como se explica a continuación:  
  
```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  
## <a name="non-microsoft-filters"></a>Filtros que no son de Microsoft
Para poder usar filtros para formatos que no son de [!INCLUDE[msCoName](../../includes/msconame-md.md)], debe cargarlos manualmente en la instancia del servidor. Para obtener información sobre cómo instalar filtros adicionales, vea [Ver o cambiar los filtros y separadores de palabras registrados](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
  
## <a name="see-also"></a>Ver también  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilidad de FILESTREAM con otras características de SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
