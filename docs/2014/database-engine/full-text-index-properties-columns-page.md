---
title: Propiedades del índice de texto completo (página columnas) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 67b7e72e0c4b248e8951667561eaf7548bfba1b5
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62778860"
---
# <a name="full-text-index-properties-columns-page"></a>Propiedades del índice de texto completo (página Columnas)
  **Para ver o cambiar las propiedades de un índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **Índice único**  
 Seleccione un índice de la lista desplegable. El índice deberá ser un índice de columna de una sola clave, único y que no admita valores NULL.  
  
 **Seleccione las columnas coincidentes que tendrán índice de texto completo**  
 La cuadrícula muestra las columnas de la tabla que están disponibles para este índice de texto completo. Se activan las columnas que tienen indización de texto completo en este momento. Opcionalmente, puede activar más columnas que desee que se indicen con texto completo.  
  
> [!IMPORTANT]  
>  Asegúrese de que al menos una columna está activada antes de hacer clic en Aceptar.  
  
|||  
|-|-|  
|**Columnas disponibles**|Nombre de columna.|  
|**Idioma del separador de palabras**|El idioma cuyos separadores de palabras y lematizadores realizan un análisis lingüístico de todos los datos indizados de texto completo.<br /><br /> Para obtener más información, vea [configurar y administrar separadores de palabras y lematizadores para la búsqueda](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) y [elegir un idioma al crear un índice de texto completo](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).|  
|**Type**|Nombre de la columna de la tabla que contiene el tipo de documento de la columna seleccionada. Se trata de una propiedad de solo lectura.|  
|**Semántica estadística**|Seleccione si desea habilitar la indización semántica para la columna seleccionada. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Si selecciona **Idioma** antes de seleccionar **Semántica estadística**y el idioma seleccionado no tiene un modelo semántico asociado, la casilla **Semántica estadística** está deshabilitada. Si selecciona **Semántica estadística** antes de seleccionar **Idioma**, los idiomas disponibles en el cuadro combinado desplegable estarán limitados a aquellos para los que exista un modelo de idioma semántico.|  
  
## <a name="see-also"></a>Consulte también  
 [Rellenar índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  
