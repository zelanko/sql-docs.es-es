---
title: Editor de lista de propiedades de búsqueda | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.spl.searchpropertylisteditor.f1
ms.assetid: 0f3ced6e-0dfd-49fc-b175-82378c3d668e
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 818e1176cb5a4f81205a36dc7be6fd9fded286ea
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773673"
---
# <a name="search-property-list-editor"></a>Editor de lista de propiedades de búsqueda
  Use este cuadro de diálogo para agregar o eliminar propiedades de búsqueda en una lista de propiedades de búsqueda.  
  
## <a name="to-use-sql-server-management-studio-to-manage-search-property-lists"></a>Para usar SQL Server Management Studio con el fin de administrar listas de propiedades de búsqueda  
 Para obtener información acerca de cómo crear, ver o eliminar una lista de propiedades de búsqueda y sobre cómo configurar un índice de texto completo para búsqueda de propiedades, vea [Search Document Properties with Search Property Lists](../relational-databases/search/search-document-properties-with-search-property-lists.md).  
  
## <a name="options"></a>Opciones  
 **Nombre de propiedad**  
 Especifique el nombre que se va a usar para identificar la propiedad en consultas de texto completo. El nombre de una propiedad puede contener espacios internos. La longitud máxima del atributo **Property Name** es de 256 caracteres. Este nombre puede ser un nombre descriptivo, como "Autor" o "Dirección particular", o bien el nombre canónico de Windows de la propiedad, como `System.Author` o `System.Contact.HomeAddress`. **Nombre de propiedad** debe identificar exclusivamente la propiedad en el conjunto de propiedades.  
  
 Los desarrolladores usan el nombre de propiedad para identificar la propiedad en el predicado [CONTAINS](/sql/t-sql/queries/contains-transact-sql) . Por tanto, cuando se agregue una propiedad es importante especificar un valor que represente significativamente la propiedad.  
  
 **GUID del conjunto de propiedades**  
 Especifique el identificador del conjunto de propiedades al que pertenece la propiedad. Se trata de un identificador único global (GUID). Un conjunto de propiedades es un grupo de propiedades relacionadas lógicamente. Para obtener más información cómo obtener este valor, vea la sección "Comentarios" más adelante en este tema.  
  
 **Identificador entero de propiedad**  
 Especifique el identificador entero de la propiedad de la propiedad. Este valor preasignado es un entero positivo que es único en el conjunto de propiedades. Para obtener más información cómo obtener este valor, vea la sección "Comentarios" más adelante en este tema.  
  
> [!NOTE]  
>  Las propiedades de documento que usan identificadores de cadena no son compatibles con la búsqueda de texto completo.  
  
 **Descripción de la propiedad**  
 Si lo desea, especifique una descripción de la propiedad. Se trata de una cadena de hasta 512 caracteres. Por ejemplo, una descripción podría contener información sobre el conjunto de propiedades o sobre una propiedad que no sea evidente a partir de su nombre.  
  
## <a name="remarks"></a>Comentarios  
 Para agregar una propiedad de búsqueda a una lista de propiedades de búsqueda, debe especificar el identificador único global (GUID) del conjunto de propiedades al que pertenezca la propiedad y el identificador entero de propiedad. Una combinación dada de estos debe ser única en una lista de propiedades de búsqueda determinada. Si intenta agregar una combinación existente, se produce un error en la operación y se emite un error. Es decir, puede configurar solo un nombre para una propiedad dada.  
  
 La descripción de la propiedad es opcional.  
  
 **Para configurar una lista de propiedades de búsqueda para un índice de texto completo**  
  
-   [Buscar propiedades de documento con listas de propiedades de búsqueda](../relational-databases/search/search-document-properties-with-search-property-lists.md)  
  
## <a name="permissions"></a>Permisos  
 Consulte [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [ALTER SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-search-property-list-transact-sql)   
 [Buscar propiedades de documento con listas de propiedades de búsqueda](../relational-databases/search/search-document-properties-with-search-property-lists.md)   
 [sys.registered_search_property_lists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-registered-search-property-lists-transact-sql)  
  
  
