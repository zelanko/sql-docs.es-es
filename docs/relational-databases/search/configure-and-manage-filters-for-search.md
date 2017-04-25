---
title: "Configurar y administrar filtros para búsquedas | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- full-text search [SQL Server], filters
- filters [full-text search]
ms.assetid: 7ccf2ee0-9854-4253-8cca-1faed43b7095
caps.latest.revision: 68
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: a9a3c108e0a9c66daa6a6cde799694ac8491e796
ms.lasthandoff: 04/11/2017

---
# <a name="configure-and-manage-filters-for-search"></a>Configurar y administrar filtros para búsquedas
  La indexación de documentos en una columna de tipo de datos **varbinary**, **varbinary(max)**, **image**o **xml** requiere un procesamiento adicional. Un filtro debe realizar este procesamiento. El filtro extrae la información de texto del documento y quita el formato. A continuación, el filtro envía el texto al componente separador de palabras correspondiente al idioma asociado a la columna de la tabla.  
  
 Un filtro determinado es específico de un tipo de documento concreto (.doc, .pdf, .xls, .xml, etc.). Estos filtros implementan la interfaz IFilter. Para obtener más información de estos tipos de documento, consulte la vista de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
 Los documentos binarios se pueden almacenar en una sola columna de tipo **varbinary(max)** o **image** . Para cada documento, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] elige el filtro correcto de acuerdo con la extensión de archivo. Dado que la extensión de archivo no está visible cuando el archivo se almacena en una columna de tipo **varbinary(max)** o **image** , la extensión de archivo (.doc, .xls, .pdf, etcétera) debe almacenarse en una columna independiente de la tabla, denominada columna de tipo. Esta columna de tipo debe ser de cualquier tipo de datos basado en caracteres y debe contener la extensión del archivo, como .doc para los documentos de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Word. En la tabla **Document** en [!INCLUDE[ssSampleDBCoShort](../../includes/sssampledbcoshort-md.md)], la columna **Document** es de tipo **varbinary(max)**y la columna de tipo **FileExtension**es de tipo **nvarchar(8)**.  
  
> [!NOTE]  
>  Un filtro podría ser capaz de tratar los incrustados en el objeto primario, dependiendo de su implementación. Sin embargo, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no configura los filtros para seguir los vínculos a otros objetos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instala sus propios filtros HTML y XML. Además, [!INCLUDE[msCoName](../../includes/msconame-md.md)] también carga los filtros para formatos de propietario de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)](.doc, .xdoc, .ppt, etcétera) que ya están instalados en el sistema operativo. Para identificar los filtros que están cargados actualmente en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use el procedimiento almacenado [sp_help_fulltext_system_components](../../relational-databases/system-stored-procedures/sp-help-fulltext-system-components-transact-sql.md) , como se explica a continuación:  
  
```  
EXEC sp_help_fulltext_system_components 'filter';   
```  
  
 Sin embargo, para poder usar filtros para formatos que no son [!INCLUDE[msCoName](../../includes/msconame-md.md)] , debe cargarlos manualmente en la instancia del servidor. Para obtener información sobre cómo instalar filtros adicionales, vea [Ver o cambiar los filtros y separadores de palabras registrados](../../relational-databases/search/view-or-change-registered-filters-and-word-breakers.md).  
  
 **Para ver la columna de tipo en un índice de texto completo existente**  
  
-   [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)  
  
## <a name="see-also"></a>Vea también  
 [sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)   
 [Compatibilidad de FILESTREAM con otras características de SQL Server](../../relational-databases/blob/filestream-compatibility-with-other-sql-server-features.md)  
  
  
