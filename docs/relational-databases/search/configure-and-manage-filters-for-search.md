---
title: Configurar y administrar filtros para búsquedas | Microsoft Docs
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: search, sql-database
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: pmasl
ms.author: pelopes
ms.reviewer: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 5dd9719ea0f10b3bbac6aae5171a2c941cdf7e1a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68093303"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurar y administrar filtros para búsquedas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  La indexación de documentos en una columna de tipo de datos **varbinary**, **varbinary(max)** , **image**, o **xml** exige un procesamiento adicional. Un filtro debe realizar este procesamiento. El filtro extrae la información de texto del documento y quita el formato. A continuación, el filtro envía el texto al componente separador de palabras correspondiente al idioma asociado a la columna de la tabla.  
 
## <a name="filters-and-document-types"></a>Tipos de documento y filtro
Un filtro determinado es específico de un tipo de documento concreto (.doc, .pdf, .xls, .xml, etc.). Estos filtros implementan la interfaz IFilter. Para obtener más información de estos tipos de documento, consulte la vista de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
Los documentos binarios se pueden almacenar en una sola columna de tipo **varbinary(max)** o **image** . Para cada documento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elige el filtro correcto de acuerdo con la extensión de archivo. Dado que la extensión de archivo no está visible cuando el archivo se almacena en una columna de tipo **varbinary(max)** o **image** , la extensión de archivo (.doc, .xls, .pdf, etcétera) debe almacenarse en una columna independiente de la tabla, denominada columna de tipo. Esta columna de tipo debe ser de cualquier tipo de datos basado en caracteres y debe contener la extensión del archivo, como .doc para los documentos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. En la tabla **Document** en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], la columna **Document** es de tipo **varbinary(max)** y la columna de tipo **FileExtension**es de tipo **nvarchar(8)** .  

**Para ver la columna de tipo en un índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
> [!NOTE]  
>  Un filtro podría ser capaz de tratar los incrustados en el objeto primario, dependiendo de su implementación. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no configura los filtros para seguir los vínculos a otros objetos.  

## <a name="installed-filters"></a>Filtros instalados 
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala sus propios filtros HTML y XML. Además, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también carga los filtros para formatos de propietario de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (.doc, .xdoc, .ppt, etcétera) que ya están instalados en el sistema operativo. Para identificar los filtros que están cargados actualmente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , como se explica a continuación:  

```sql
EXEC sp_help_fulltext_system_components 'filter';   
```  

> [!NOTE]
> Incluso con la versión más reciente del módulo Filter Pack de Office que proporciona compatibilidad con .xlsx, SQL Server no admite hojas de cálculo Strict Open XML.  No se devolverá ningún error, simplemente se producirá un error en SQL Server al indexar el contenido de cualquier hoja de cálculo Strict Open XML.

## <a name="non-microsoft-filters"></a>Filtros que no son de Microsoft
Para poder usar filtros para formatos que no son de [!INCLUDE[msCoName](../../includes/msconame-md.md)], debe cargarlos manualmente en la instancia del servidor. Para obtener información sobre cómo instalar filtros adicionales, vea [Ver o cambiar los filtros y separadores de palabras registrados](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
  
## <a name="see-also"></a>Consulte también  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilidad de FILESTREAM con otras características de SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
