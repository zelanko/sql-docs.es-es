---
title: Operadores de filtro (Master Data Services) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: mds
ms.service: 
ms.component: non-specific
ms.reviewer: 
ms.suite: sql
ms.technology:
- master-data-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 27914c8b-8951-4b7d-914d-1cbf528dd248
caps.latest.revision: 
author: leolimsft
ms.author: lle
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 7d398e710708cceea613fb5cbca0500bf5d3b8da
ms.sourcegitcommit: 6ac1956307d8255dc544e1063922493b30907b80
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/05/2018
---
# <a name="filter-operators-master-data-services"></a>Operadores de filtro (Master Data Services)
  Al filtrar una lista de miembros, están disponibles los operadores siguientes.  
  
> [!NOTE]  
>  Cuando se filtra por varios criterios, deben cumplirse todos los criterios para que se devuelvan resultados. Por ejemplo, SquareFeet = 2000 **AND** Division <> 123.  
  
## <a name="filter-operators"></a>Operadores de filtro  
  
|Nombre del control|Description|  
|------------------|-----------------|  
|**Es igual que**|Devuelve valores de atributo que son exactamente iguales que los criterios especificados. Por ejemplo, para filtrar según **Mountain-100**, debe escribir **Mountain-100**.|  
|**No es igual que**|Devuelve valores de atributo que no son exactamente iguales a los criterios especificados. Los criterios de filtro deben ser exactamente iguales que el valor de atributo que desea omitir en los resultados. Por ejemplo, para omitir resultados que coincidan con **Mountain-100**, debe escribir **Mountain-100**.<br /><br /> <br /><br /> Nota: Al aplicar una condición de filtro con una cláusula "no es igual" en un atributo, un miembro para el que el atributo es NULL pasará la condición de filtro y se devolverá si SET ANSI_NULLS está establecido en ON en la configuración de la base de datos. Para detener este comportamiento, establezca SET ANSI_NULLS en OFF en la configuración de la base de datos. Cuando SET ANSI_NULLS se establece en OFF, las comparaciones de todos los datos con un valor NULL se evalúan en TRUE si el valor de los datos es NULL, con el resultado de que el miembro no pasaría la cláusula “no es igual”. Para obtener más información, vea [SET ANSI_NULLS &#40;Transact-SQL&#41;](../t-sql/statements/set-ansi-nulls-transact-sql.md).|  
|**Es como**|Usa el operador LIKE de Transact-SQL para filtrar los resultados. Para más información, vea [LIKE &#40;Transact-SQL&#41;](../t-sql/language-elements/like-transact-sql.md) en los Libros en pantalla de SQL Server.|  
|**No es como**|Utiliza al operador NOT de Transact-SQL para filtrar los resultados. Para más información, vea [NOT &#40;Transact-SQL&#41;](../t-sql/language-elements/not-transact-sql.md) en los Libros en pantalla de SQL Server.|  
|**Es mayor que**|Devuelve valores de atributo que son mayores que los criterios especificados. Por ejemplo, para devolver valores de atributo que comiencen con una letra en una posición posterior a **F**, escriba **F**.|  
|**Es menor que**|Devuelve valores de atributo que son menores que los criterios especificados. Por ejemplo, para devolver valores de atributo que comiencen con una letra en una posición anterior a **F**, escriba **F**.|  
|**Es mayor o igual que**|Devuelve valores de atributo que son mayores o iguales que los criterios especificados. Por ejemplo, para devolver valores de atributo que comiencen con el número **3** o un número mayor, escriba **3**.|  
|**Es menor o igual que**|Devuelve valores de atributo que son menores o iguales que los criterios especificados. Por ejemplo, para devolver valores de atributo que comiencen con el número **3** o un número menor, escriba **3**.|  
|**Coincide**|Utiliza un índice de búsquedas aproximadas para filtrar los resultados.<br /><br /> Use el campo **Nivel de similitud** para especificar la aproximación de la coincidencia de los valores de atributo con respecto a los criterios de filtro (con un valor predeterminado del 30 %).<br /><br /> Seleccione una de las siguientes opciones en el cuadro de lista **Algoritmo** :<br /><br /> **Levenshtein**: una distancia que se basa en el número de modificaciones (por ejemplo, adiciones o eliminaciones) necesarias para que una cadena coincida con otra. Ésta es la opción predeterminada. No requiere ningún parámetro adicional.<br /><br /> **Jaccard**: un índice que resulta óptimo cuando se intentan comparar varias cadenas. Esta búsqueda admite un parámetro adicional de compensación de contención (vea más abajo).<br /><br /> **Jaro-Winkler**: una distancia óptima para buscar nombres de persona duplicados. Este método devuelve más resultados que cualquier otro método. No admite compensación de contención.<br /><br /> **Subsecuencia común más larga**: los trabajos basados en una subsecuencia en la que las letras de un patrón aparecen en orden, pese a que se pueden separar (por ejemplo, "MSR" es una subsecuencia de "MaSteR"). Esta búsqueda admite un parámetro adicional de compensación de contención (vea más abajo).<br /><br /> <br /><br /> Nota: Agregue una **Compensación de contención** para los algoritmos **Jaccard** o **Subsecuencia común más larga**. Se trata de un umbral de longitud que se proporcionada en un porcentaje decimal entre 0 y 1, con un valor predeterminado de 0,62. Un umbral inferior aumentaría el número de coincidencias posibles devueltas.|  
|**No coincide**|Utiliza un índice de búsquedas aproximadas para filtrar los resultados. Utilice el campo **Nivel de similitud** para especificar la aproximación de la falta de coincidencia de los valores de atributo con respecto a los criterios de filtro.|  
|**Contiene el patrón**|Utiliza las expresiones regulares de .NET Framework para filtrar los resultados en un patrón especificado. Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](http://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.|  
|**No contiene patrón**|Utiliza las expresiones regulares de .NET Framework para filtrar los resultados que no coinciden con un patrón especificado. Para obtener más información sobre las expresiones regulares, consulte [Elementos del lenguaje de expresiones regulares](http://go.microsoft.com/fwlink/?LinkId=164401) en MSDN Library.|  
|**Es NULL**|Devuelve valores de atributo que son NULL. El campo **Criterios** se deshabilita cuando selecciona el operador **Es NULL** .|  
|**No es NULL**|Devuelve valores de atributo que no son NULL. El campo **Criterios** se deshabilita cuando selecciona el operador **No es NULL** .|  
  
  
