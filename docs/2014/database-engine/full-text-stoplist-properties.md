---
title: Propiedades de lista de palabras irrelevantes de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftstoplistproperties.general.f1
- sql12.swb.fulltextsearch.ftstoplistproperties.schedule.f1
ms.assetid: 2e907f5b-0cf9-484a-afcf-a4e7f1e2f87f
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 4cfdd308ab7488633721ddaac55d3d926a276b0d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62779412"
---
# <a name="full-text-stoplist-properties"></a>Propiedades de lista de palabras irrelevantes de texto completo
  Use este cuadro de diálogo para agregar o eliminar palabras irrelevantes individuales, eliminar todas las palabras irrelevantes para un idioma concreto o borrar la lista de palabras irrelevantes actual. Una palabra irrelevante es una palabra de uso frecuente que se incluye en una lista de palabras irrelevantes. Las palabras irrelevantes de una lista de palabras irrelevantes se omiten en la indización de texto completo para las tablas que usan dicha lista. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../relational-databases/search/full-text-search.md).  
  
 **Para usar SQL Server Management Studio a fin de modificar las propiedades de la lista de palabras irrelevantes**  
  
-   [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](../relational-databases/search/full-text-search.md)  
  
## <a name="options"></a>Opciones  
 **Acción**  
 Especifica la acción que desea realizar.  
  
 **Agregar palabra irrelevante**  
 Agrega una palabra de uso frecuente a la lista de palabras irrelevantes.  
  
 **Eliminar palabra irrelevante**  
 Elimina una palabra irrelevante de la lista de palabras irrelevantes.  
  
 **Eliminar todas las palabras irrelevantes**  
 Elimina todas las palabras irrelevantes para un idioma concreto.  
  
 **Borrar lista de palabras irrelevantes**  
 Borra la lista de palabras irrelevantes eliminando todas las palabras irrelevantes para todos los idiomas.  
  
 **Palabra irrelevante**  
 Si seleccionó **Agregar palabra irrelevante** o **Eliminar palabra irrelevante**, escriba la palabra irrelevante en el campo **Palabra irrelevante** . Una nueva palabra irrelevante debe ser única; es decir, no debe estar todavía en esta lista de palabras irrelevantes para el idioma que seleccione.  
  
 **Idioma de texto completo**  
 Si seleccionó **Agregar palabra irrelevante**, **Eliminar palabra irrelevante**o **Eliminar todas las palabras irrelevantes**, seleccione el idioma de la palabra o palabras irrelevantes en el cuadro de lista. Este cuadro incluye todos los idiomas de texto completo compatibles con la instancia de servidor.  
  
## <a name="see-also"></a>Consulte también  
 [Sys. fulltext_stopwords &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stopwords-transact-sql)   
 [Sys. fulltext_stoplists &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-fulltext-stoplists-transact-sql)   
 [Configurar y administrar palabras irrelevantes y palabras irrelevantes para la búsqueda de texto completo](../relational-databases/search/full-text-search.md)   
 [ALTER FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-fulltext-stoplist-transact-sql)   
 [CREATE FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-fulltext-stoplist-transact-sql)   
 [DROP FULLTEXT STOPLIST &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-fulltext-stoplist-transact-sql)  
  
  
