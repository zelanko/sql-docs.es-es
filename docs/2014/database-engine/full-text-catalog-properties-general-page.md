---
title: Propiedades del catálogo de texto completo (página General) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: be73ed98700ef261ccee026469dddd22017998e0
ms.sourcegitcommit: aa4f594ec6d3e85d0a1da6e69fa0c2070d42e1d8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/08/2019
ms.locfileid: "59241455"
---
# <a name="full-text-catalog-properties-general-page"></a>Propiedades del catálogo de texto completo (página General)
  En esta sección se muestran las opciones y funciones disponibles en la página **General** del cuadro de diálogo **Propiedades del catálogo de texto completo** .  
  
> [!NOTE]  
>  En las bases de datos de [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , un catálogo de texto completo es un concepto lógico que hace referencia a un grupo de índices de texto completo. Un catálogo de texto completo es un objeto virtual y no pertenece a ningún grupo de archivos.  
  
## <a name="options"></a>Opciones  
  
### <a name="properties"></a>Propiedades  
 **Catálogo predeterminado**  
 Muestra si el catálogo es el predeterminado de la base de datos.  
  
 **Estado del rellenado**  
 Indica el estado del catálogo. Los valores posibles son:  
  
-   **Idle**  
  
-   **Rastreo en curso**  
  
-   **En pausa**  
  
-   **Acelerado**  
  
-   **Recuperando**  
  
-   **Apagar**  
  
-   **Rellenado incremental en curso**  
  
-   **Generando índice**  
  
-   **El disco está en pausa el completo**  
  
-   **seguimiento de cambios**  
  
 **Recuento de elementos**  
 Muestra el número de elementos de texto completo del catálogo.  
  
 **Tamaño del catálogo**  
 Muestra el tamaño del catálogo de texto completo en megabytes.  
  
 **Nombre**  
 Nombre del catálogo de texto completo.  
  
 **Distinguir acentos**  
 Vea o modifique si el catálogo distingue las marcas diacríticas, como la tilde (**~**), el acento agudo (**'**) o la diéresis (**¨**). Los valores válidos son:  
  
-   **No**  
  
-   **Sí**  
  
-   Para obtener información acerca de las marcas diacríticas, vea [diacrítico](https://www.merriam-webster.com/dictionary/diacritic) en el diccionario Merriam Webster.  
  
 **Fecha del último rellenado**  
 Muestra la fecha de la última vez que se rellenó el catálogo.  
  
 **Propietario**  
 Propietario del catálogo de texto completo.  
  
 **Recuento de claves únicas**  
 Número de palabras únicas que componen el índice de texto completo del catálogo.  
  
### <a name="catalog-action"></a>Acción del catálogo  
  
|||  
|-|-|  
|**None**|No realiza las operaciones **Optimizar catálogo**, **Volver a generar el catálogo**ni **Volver a llenar el catálogo** .|  
|**Optimizar catálogo**|Optimiza el uso de espacio del catálogo y mejora el rendimiento de las consultas. También mejora la precisión de la clasificación de los aciertos de los resultados de las búsquedas.<br /><br /> Esta acción ejecuta ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE.|  
|**Volver a generar el catálogo**|Elimina el catálogo de texto completo y lo genera de nuevo. Esta operación debe realizarse si se modifica una propiedad básica del catálogo, como la distinción de acentos.<br /><br /> Para que el catálogo se genere correctamente, el grupo de archivos en el que reside el catálogo de texto completo debe estar en línea o tener el acceso de lectura y escritura activado. Después de la regeneración, se volverá a llenar el índice de texto completo.<br /><br /> Esta acción ejecuta ALTER FULLTEXT CATALOG *catalog_name* REBUILD.|  
|**Volver a llenar el catálogo**|Actualiza el catálogo con los cambios recientes realizados en los datos. Para esta opción, el catálogo debe estar inactivo.|  
  
## <a name="see-also"></a>Vea también  
 [Rellenar índices de texto completo](../relational-databases/indexes/indexes.md)  
  
  
