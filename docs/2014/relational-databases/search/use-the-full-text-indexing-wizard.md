---
title: Usar el Asistente para indización de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: search
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextindexingwizard.selecttablecolumns.f1
- sql12.swb.fulltextindexingwizard.welcome.f1
- sql12.swb.fulltextindexingwizard.selectacatalog.f1
- sql12.swb.fulltextindexingwizard.progress.f1
- sql12.swb.fulltextindexingwizard.selectorcreatepopschedules.f1
- sql12.swb.fulltextindexingwizard.selectatableorview.f1
- sql12.swb.fulltextindexingwizard.selectchangetracking.f1
- sql12.swb.fulltextindexingwizard.selectanindex.f1
- sql12.swb.fulltextindexingwizard.summary.f1
helpviewer_keywords:
- Full-Text Indexing Wizard
- full-text search [SQL Server], Full-Text Indexing Wizard
ms.assetid: 3e9d9605-6525-4781-9168-fdaa06db3459
caps.latest.revision: 22
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5395a6ee63d3fbf4456a3da4e4e19390e042e2b4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37309525"
---
# <a name="use-the-full-text-indexing-wizard"></a>Usar el Asistente para indización de texto completo
  El Asistente para indización de texto completo le guía por una serie de pasos diseñados para ayudarle a crear un índice de texto completo.  
  
#### <a name="to-use-the-full-text-indexing-wizard"></a>Para usar el Asistente para indización de texto completo  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en la tabla en la que quiere crear un índice de texto completo, seleccione **Índice de texto completo**y, luego, haga clic en **Definir índice de texto completo**.  
  
     **Índice único**  
     Seleccione un índice de la lista desplegable. El índice deberá ser un índice de columna de una sola clave, único y que no admita valores NULL. Seleccione el índice de clave única más pequeño para la clave única de texto completo. Para obtener mejores resultados, se recomienda utilizar un índice clúster.  
  
     **Columnas disponibles**  
     Para incluir una columna en el índice, active la casilla situada junto al nombre de columna. Las columnas que no son aptas para la indización de texto completo aparecen en gris con las casillas deshabilitadas.  
  
     **Idioma para el separador de palabras**  
     Seleccione un idioma en la lista desplegable. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizará esta opción para identificar los separadores de palabras correctos para el índice. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa separadores de palabras para identificar límites de palabras en los datos indexados de texto completo.  
  
     **Columna de tipo**  
     Seleccione el nombre de la columna que incluye el tipo de documento de la columna que se va a incluir en el índice de texto completo.  
  
     El **columna de tipo** solo se habilita cuando la columna mencionada en el **columnas disponibles** columna es de tipo `varbinary(max)` o `image`.  
  
     **Semántica estadística**  
     Seleccione si desea habilitar la indización semántica para la columna seleccionada. Para obtener más información, vea [Búsqueda semántica &#40;SQL Server&#41;](semantic-search-sql-server.md).  
  
     Si selecciona **Idioma** antes de seleccionar **Semántica estadística**y el idioma seleccionado no tiene un modelo semántico asociado, la casilla **Semántica estadística** está deshabilitada. Si selecciona **Semántica estadística** antes de seleccionar **Idioma**, los idiomas disponibles en el cuadro combinado desplegable estarán limitados a aquellos para los que exista un modelo de idioma semántico.  
  
2.  Seleccione las opciones de seguimiento de cambios.  
  
     **Automáticamente**  
     Seleccione este botón de opción para que el índice de texto completo se actualice automáticamente cuando se produzcan cambios en los datos subyacentes.  
  
     **Manualmente**  
     Seleccione este botón de opción si no desea que el índice de texto completo se actualice automáticamente cuando se produzcan cambios en los datos subyacentes. Los cambios en los datos se mantienen; sin embargo, para aplicarlos al índice de texto completo es necesario iniciar o programar este proceso manualmente.  
  
     **No realizar seguimiento de cambios**  
     Seleccione este botón de opción si no desea que el índice de texto completo se actualice con los cambios en los datos subyacentes.  
  
     **Iniciar llenado completo al crea el índice**  
     Seleccione este botón de opción para iniciar un llenado completo tras la finalización correcta de este asistente. De esta forma, se creará la estructura del índice de texto completo en el catálogo y se llenará con los datos indizados de texto completo.  
  
3.  Seleccione el catálogo, el grupo de archivos de índice y la lista de palabras irrelevantes.  
  
     **Seleccionar catálogo de texto completo**  
     Seleccione un catálogo de texto completo de la lista. El catálogo predeterminado de la base de datos será el elemento seleccionado de manera predeterminada en la lista. Si no hay catálogos disponibles, la lista estará deshabilitada y la casilla **Crear un nuevo catálogo** estará activada y deshabilitada.  
  
    |||  
    |-|-|  
    |**Crear un nuevo catálogo**|Seleccione esta opción para crear un nuevo catálogo de texto completo.|  
  
     **Nombre**  
     Escriba un nombre para el nuevo catálogo de texto completo.  
  
     **Establecer como catálogo predeterminado**  
     Seleccione esta opción para hacer que el catálogo sea el valor predeterminado para esta base de datos.  
  
     **Distinción de acentos**  
     Especifique si el nuevo catálogo distinguirá acentos. Si la base de datos distingue acentos, la opción **Con distinción** estará seleccionada de manera predeterminada.  
  
     **Seleccionar grupo de archivos de índice**  
     Especifique el grupo de archivos en el que crear el índice de texto completo.  
  
     Seleccione uno de los siguientes valores:  
  
    |Valor|Descripción|  
    |-----------|-----------------|  
    |**\<predeterminada >**|Si la tabla o la vista no tienen particiones, seleccione este valor para usar el mismo grupo de archivos que la tabla o vista subyacente. Si la tabla o la vista tienen particiones, se usa el grupo de archivos principal.|  
    |**PRIMARY**|Seleccione este valor para usar el grupo de archivos principal para el nuevo índice de texto completo.|  
    |*grupo de archivos predeterminado especificado por el usuario*|Si existe una lista de palabras irrelevantes predeterminada definida por el usuario, seleccione su nombre en la lista con el fin de utilizar ese grupo de archivos para el nuevo índice de texto completo.|  
  
     **Seleccionar lista de palabras irrelevantes de texto completo**  
     Especifique una lista de palabras irrelevantes para usarla en el índice de texto completo, o deshabilite el uso de la lista de palabras irrelevantes.  
  
     En [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] y versiones posteriores, las palabras irrelevantes se administran en bases de datos que usan objetos denominados listas de palabras irrelevantes. Una *lista de palabras irrelevantes* es una lista de palabras que, cuando se asocia a un índice de texto completo, se aplica a las consultas de texto completo en ese índice. Para obtener más información, vea [Configurar y administrar palabras irrelevantes y listas de palabras irrelevantes para la búsqueda de texto completo](configure-and-manage-stopwords-and-stoplists-for-full-text-search.md).  
  
     Seleccione uno de los siguientes valores:  
  
    |Valor|Descripción|  
    |-----------|-----------------|  
    |**\<sistema >**|Seleccione este valor para utilizar la lista de palabras irrelevantes del sistema en el nuevo índice de texto completo. Este es el valor predeterminado.|  
    |**\<desactivar >**|Seleccione este valor para deshabilitar las listas de palabras irrelevantes para el nuevo índice de texto completo.|  
    |*user-defined-stoplist-name*|La lista muestra el nombre de cada lista de palabras irrelevantes definida por el usuario, si hay alguna, que se haya creado en la base de datos. Seleccione la lista de palabras irrelevantes definida por el usuario que desee para utilizarla para el nuevo índice de texto completo.|  
  
4.  Opcionalmente, defina la programación de rellenado. Las operaciones de indización comenzarán inmediatamente, a menos que se hayan programado para que se ejecuten posteriormente. Las programaciones se crearán inmediatamente, aunque no se ejecuten hasta la hora programada.  
  
     **Nueva programación de tabla**  
     Permite definir una programación de llenado para una tabla.  
  
     **Nueva programación de catálogo**  
     Permite definir una programación de llenado para un catálogo de texto completo.  
  
     **Editar**  
     Permite editar una programación.  
  
     **Eliminar**  
     Permite eliminar una programación.  
  
5.  Vea o controle el progreso del Asistente para indización de texto completo.  
  
     **Detener**  
     Interrumpe la operación actual e impide que el asistente lleve a cabo operaciones de texto completo posteriores durante esta sesión.  
  
     **Informe**  
     Cuando finalice la ejecución de todas las operaciones, haga clic en este botón para obtener acceso a un informe sobre las operaciones efectuadas. Puede ver el informe, imprimirlo en un archivo, copiarlo al portapapeles o enviarlo por correo electrónico.  
  
  
