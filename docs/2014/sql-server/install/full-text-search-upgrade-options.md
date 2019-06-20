---
title: Opciones de actualización de búsqueda de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- Full-Text Search
- Upgrade options, Full-Text Search
ms.assetid: 16c9376b-5fbb-4495-a429-06a2493849c9
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: 575105d61446f2fd272e4087457e7762c1abb2e8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66095086"
---
# <a name="full-text-search-upgrade-options"></a>Opciones de actualización de búsqueda de texto completo
  Use la página de opciones de actualización de búsqueda de texto completo del Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para seleccionar la opción de actualización de búsqueda de texto completo que usará con las bases de datos cuya actualización está realizando en este momento.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] , cada índice de texto completo reside en un catálogo de texto completo que pertenece a un grupo de archivos, tiene una ruta de acceso física y es tratado como un archivo de base de datos. Ahora, un catálogo de texto completo es un objeto lógico de un concepto virtual-que hace referencia a un grupo de índices de texto completo. Por consiguiente, no se trata a cada nuevo catálogo de texto completo como un archivo de base de datos con una ruta de acceso física. Sin embargo, durante la actualización de cualquier catálogo de texto completo que contiene archivos de datos, se crea un nuevo grupo de archivos en el mismo disco. Esto conserva el comportamiento de E/S del disco antiguo después de la actualización. Si la ruta de acceso raíz existe, todos los índices de texto completo del catálogo se situarán en el nuevo grupo de archivos. Si la ruta de acceso al catálogo de texto completo antiguo no es válida, la actualización mantiene el índice de texto completo en el mismo grupo de archivos que la tabla base o, si se trata de una tabla con particiones, en el grupo de archivos principal.  
  
## <a name="options"></a>Opciones  
 Al actualizar a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], elija una de las opciones de actualización de texto completo siguientes.  
  
 **Importar**  
 Se importan los catálogos de texto completo. Normalmente, el proceso de importación es significativamente más rápido que el de regeneración. Por ejemplo, si se usa solo una CPU, importar es aproximadamente 10 veces más rápido que volver a generar. Sin embargo, un catálogo de texto completo importado desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] no usa los separadores de palabras nuevos y mejorados, por lo que es posible que, al final, le interese volver a generar los catálogos de texto completo.  
  
> [!NOTE]  
>  La recompilación se puede ejecutar en modo de varios subprocesos; además, si hay más de 10 CPU disponibles y permite que el proceso de recompilación las use todas, dicho proceso puede resultar más rápido que el de importación.  
  
 Si un catálogo de texto completo no está disponible, se vuelven a generar los índices de texto completo asociados. Esta opción solo está disponible para bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] .  
  
 Para obtener información sobre el impacto de importar un índice de texto completo, vea "Consideraciones sobre la elección de una opción de actualización de texto completo" más adelante en este tema.  
  
 **Volver a generar**  
 Los catálogos de texto completo se vuelven a generar con los separadores de palabras nuevos y mejorados. El proceso de recompilación de los índices puede llevar mucho tiempo y podría ser necesaria una cantidad significativa de CPU y de memoria después de la actualización.  
  
 **Restablecer**  
 Los catálogos de texto completo se restablecen. Cuando se actualizan desde [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], los catálogos de texto completo se quitan, pero los metadatos de los catálogos de texto completo y los índices de texto completo se conservan. Después de actualizarse, todos los índices de texto completo quedan deshabilitados para el seguimiento de cambios y los rastreos no se inician de forma automática. El catálogo permanecerá vacío hasta que se emita manualmente un rellenado completo después de que se complete la actualización.  
  
 Todas estas opciones de actualización permiten asegurarse de que las bases de datos actualizadas se benefician de las mejoras en el rendimiento del texto completo.  
  
## <a name="considerations-for-choosing-a-full-text-upgrade-option"></a>Consideraciones sobre la elección de una opción de actualización de texto completo  
 Cuando elija la opción de actualización, tenga en cuenta lo siguiente:  
  
-   ¿Cómo usa los separadores de palabras?  
  
     El servicio de búsqueda de texto completo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] incluye nuevos separadores de palabras y lematizadores. Estos podrían cambiar los resultados de las consultas de texto completo llevadas a cabo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] para un determinado escenario o patrón de texto. Por tanto, a la hora de elegir una opción de actualización adecuada, es importante que tenga en cuenta el uso que va a dar a los separadores de palabras:  
  
    -   Si los separadores de palabras del idioma de texto completo que usa no han cambiado o, si la precisión de la recuperación no le parece importante, la importación es una opción adecuada. Más adelante, si experimenta problemas de recuperación y desea actualizar a los nuevos separadores de palabras, solo tendrá que volver a generar los catálogos de texto completo.  
  
    -   Si le preocupa la precisión de la recuperación y usa uno de los separadores de palabras que se agregaron después de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], la regeneración es la opción adecuada.  
  
-   ¿Se han generado índices de texto completo en columnas de clave de texto completo cuyo tipo de datos es Integer?  
  
     La regeneración realiza optimizaciones internas que, en algunos casos, mejoran el rendimiento de las consultas del índice de texto completo actualizado. En concreto, si tiene catálogos de texto completo que contienen índices de texto completo para los que la columna de clave de texto completo de la tabla base es un tipo de datos Integer, al volver a generarlos, se logra un rendimiento ideal de las consultas de texto completo después de la actualización. En este caso, es muy recomendable el uso de la opción **Volver a generar** .  
  
    > [!NOTE]  
    >  Para los índices de texto completo de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], se recomienda que el tipo de datos de la columna que actúa como clave de texto completo sea Integer. Para obtener más información, vea [Mejorar el rendimiento de los índices de texto completo](../../relational-databases/indexes/indexes.md).  
  
-   ¿Cuál es la prioridad para poner en línea la instancia del servidor?  
  
     El proceso de importación o regeneración durante la actualización consume muchos recursos de la CPU, lo que retrasa la actualización y puesta en línea del resto de la instancia del servidor. Si es importante poner en línea lo antes posible la instancia del servidor y desea ejecutar manualmente el rellenado después de la actualización, la opción **Restablecer** resulta adecuada.  
  
## <a name="additional-resources"></a>Recursos adicionales  
  
