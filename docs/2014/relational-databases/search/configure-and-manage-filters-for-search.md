---
title: Configurar y administrar filtros para búsquedas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e9a57c95226a9b277cfb718b40b5d0525b1f8eb3
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "84997747"
---
# <a name="configure-and-manage-filters-for-search"></a>Configurar y administrar filtros para búsquedas
  Indizar los documentos de una columna de los tipos de datos `varbinary`, `varbinary(max)`, `image` o `xml` requiere procesamiento adicional. Un filtro debe realizar este procesamiento. El filtro extrae la información de texto del documento y quita el formato. A continuación, el filtro envía el texto al componente separador de palabras correspondiente al idioma asociado a la columna de la tabla.  
  
 Un filtro determinado es específico de un tipo de documento concreto (.doc, .pdf, .xls, .xml, etc.). Estos filtros implementan la interfaz IFilter. Para obtener más información de estos tipos de documento, consulte la vista de catálogo [sys.fulltext_document_types](/sql/relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql) .  
  
 Los documentos binarios se pueden almacenar en una sola columna de tipo  `varbinary(max)` o `image`. Para cada documento, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] elige el filtro correcto de acuerdo con la extensión de archivo. Dado que la extensión de archivo no está visible cuando el archivo se almacena en una `varbinary(max)` `image` columna o, la extensión de archivo (. doc,. xls,. pdf, etc.) debe almacenarse en una columna independiente de la tabla, denominada columna de tipo. Esta columna de tipo debe ser de cualquier tipo de datos basado en caracteres y debe contener la extensión del archivo, como .doc para los documentos de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Word. En la tabla **Document** en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)] , la columna **Document** es de tipo `varbinary(max)` y la columna Type, **FileExtension**, es de tipo `nvarchar(8)` .  
  
> [!NOTE]  
>  Un filtro podría ser capaz de tratar los incrustados en el objeto primario, dependiendo de su implementación. Sin embargo, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no configura los filtros para seguir los vínculos a otros objetos.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instala sus propios filtros HTML y XML. Además, [!INCLUDE[msCoName](../../../includes/msconame-md.md)] también carga los filtros para formatos de propietario de  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)](.doc, .xdoc, .ppt, etcétera) que ya están instalados en el sistema operativo. Para identificar los filtros que están cargados actualmente en una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_help_fulltext_system_components](/sql/relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql) , como se explica a continuación:  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 Sin embargo, para poder usar filtros para formatos que no son [!INCLUDE[msCoName](../../../includes/msconame-md.md)] , debe cargarlos manualmente en la instancia del servidor. Para obtener información sobre cómo instalar filtros adicionales, vea [Ver o cambiar los filtros y separadores de palabras registrados](view-or-change-registered-filters-and-word-breakers.md).  
  
 **Para ver la columna de tipo en un índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)  
  
## <a name="see-also"></a>Consulte también  
 [Sys. fulltext_index_columns &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql)   
 [Compatibilidad de FILESTREAM con otras características de SQL Server](../blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
