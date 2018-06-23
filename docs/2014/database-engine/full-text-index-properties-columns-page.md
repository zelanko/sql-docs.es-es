---
title: Propiedades del índice de texto completo (página columnas) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.fulltextsearch.fulltextindexproperties.columns.f1
ms.assetid: 75e52edb-0d07-4393-9345-8b5af4561e35
caps.latest.revision: 17
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 223a3e0db58b73f2b841cebd23d41bc36ba4a85b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36106409"
---
# <a name="full-text-index-properties-columns-page"></a>Propiedades del índice de texto completo (página Columnas)
  **Para ver o cambiar las propiedades de un índice de texto completo**  
  
-   [Administrar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
## <a name="uielement-list"></a>Lista de UIElement  
 **índice único**  
 Seleccione un índice de la lista desplegable. El índice deberá ser un índice de columna de una sola clave, único y que no admita valores NULL.  
  
 **Seleccione las columnas coincidentes que serán el índice de texto completo**  
 La cuadrícula muestra las columnas de la tabla que están disponibles para este índice de texto completo. Se activan las columnas que tienen indización de texto completo en este momento. Opcionalmente, puede activar más columnas que desee que se indicen con texto completo.  
  
> [!IMPORTANT]  
>  Asegúrese de que al menos una columna está activada antes de hacer clic en Aceptar.  
  
|||  
|-|-|  
|**Columnas disponibles**|Nombre de columna.|  
|**Idioma del separador de palabras de**|El idioma cuyos separadores de palabras y lematizadores realizan un análisis lingüístico de todos los datos indizados de texto completo.<br /><br /> Para obtener más información, consulte [configurar y administrar separadores de palabras y lematizadores para la búsqueda](../relational-databases/search/configure-and-manage-word-breakers-and-stemmers-for-search.md) y [elegir un idioma al crear un índice de texto completo](../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).|  
|**Tipo**|Nombre de la columna de la tabla que contiene el tipo de documento de la columna seleccionada. Se trata de una propiedad de solo lectura.|  
|**Semántica estadística**|Seleccione si desea habilitar la indización semántica para la columna seleccionada. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](../relational-databases/search/semantic-search-sql-server.md).<br /><br /> Si selecciona **Idioma** antes de seleccionar **Semántica estadística**y el idioma seleccionado no tiene un modelo semántico asociado, la casilla **Semántica estadística** está deshabilitada. Si selecciona **Semántica estadística** antes de seleccionar **Idioma**, los idiomas disponibles en el cuadro combinado desplegable estarán limitados a aquellos para los que exista un modelo de idioma semántico.|  
  
## <a name="see-also"></a>Vea también  
 [Rellenar índices de texto completo](../relational-databases/search/populate-full-text-indexes.md)  
  
  