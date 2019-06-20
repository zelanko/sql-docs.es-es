---
title: Buscar en documentos mediante las listas de resultados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- searches [SQL Server Management Studio], result lists
- result list searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], multiple files
- Query Editor [SQL Server Management Studio], search multiple files
ms.assetid: 275e1b6c-fbd0-4408-af77-35903f90657c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 957b6e46cb8c3b4cc551c616a1b547c3c1cbdeb1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66090159"
---
# <a name="search-documents-using-results-lists"></a>Buscar en documentos mediante las listas de resultados
  Con el cuadro de diálogo **Buscar y reemplazar** es posible buscar y reemplazar texto en todos los archivos de un proyecto o una solución, o en una carpeta del sistema de archivos, aunque no estén abiertos en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Las coincidencias de las búsquedas realizadas con el cuadro de diálogo **Buscar y reemplazar** aparecen en las ventanas Resultados de la búsqueda 1 y Resultados de la búsqueda 2, que permiten ver el texto exacto de la línea que contiene la coincidencia.  
  
### <a name="to-search-in-multiple-files"></a>Para buscar en varios archivos  
  
1.  En el menú **Editar** , elija **Buscar y reemplazar** y, a continuación, haga clic en **Buscar en archivos**.  
  
2.  En el cuadro de texto **Buscar** , escriba el texto que desea buscar.  
  
3.  En la lista **Buscar en** , haga clic en **Todos los documentos abiertos**, **Proyecto actual**, **Toda la solución**o especifique una ruta de acceso.  
  
4.  En la lista **Tipos de archivo** , seleccione uno de los conjuntos enumerados de extensiones de archivo o especifique las extensiones de los tipos de archivo que desea buscar, separadas por signos de punto y coma. Utilice \*.\* para buscar todos los archivos del directorio que aparece en la lista desplegable **Buscar en** .  
  
5.  Elija las opciones de búsqueda restantes para aumentar la precisión de la misma.  
  
6.  Haga clic en **Buscar** para iniciar la búsqueda.  
  
 Las coincidencias de la búsqueda aparecen, de forma predeterminada, en la ventana Resultados de la búsqueda 1. Puede examinar las coincidencias de la búsqueda si hace doble clic en cada entrada de la ventana Resultados de la búsqueda 1. Para ver los resultados de la búsqueda en una ventana nueva, seleccione **Mostrar resultados en otra ventana**.  
  
#### <a name="to-replace-across-multiple-files-or-folders"></a>Para reemplazar en varios archivos o carpetas  
  
1.  En el menú **Editar** , elija **Buscar y reemplazar** y, a continuación, haga clic en **Reemplazar en archivos**.  
  
2.  En el cuadro de texto **Buscar** , escriba el texto que desea buscar.  
  
3.  En el cuadro **Reemplazar con** , escriba el texto que reemplazará al texto de la búsqueda.  
  
4.  En la lista **Buscar en** , haga clic en **Todos los documentos abiertos**, **Proyecto actual**, **Toda la solución**o especifique una ruta de acceso.  
  
5.  Haga clic en **Reemplazar** para reemplazar el texto de búsqueda con el texto del cuadro **Reemplazar con** . Puede omitir una coincidencia específica si hace clic en **Buscar siguiente** o un archivo entero si hace clic en **Omitir archivo**.  
  
     \- O bien  
  
     Elija **Reemplazar todo** para reemplazar todas las coincidencias de búsqueda con el texto del cuadro **Reemplazar con** . Si desea deshacer algunos de los reemplazos en otro momento, seleccione **Mantener los archivos modificados abiertos después de Reemplazar todo** .  
  
    > [!NOTE]  
    >  **Reemplazar todo** reemplaza todas las coincidencias de la búsqueda, incluidas aquellas que se encuentran en archivos que se han omitido mediante **Omitir archivo** o **Buscar siguiente**. Solo es posible utilizar **Deshacer** en los reemplazos realizados en archivos que permanecen abiertos tras la operación de reemplazo.  
  
 La información de reemplazo aparece de forma predeterminada en la ventana Resultados de la búsqueda 1. Puede examinar los reemplazos si hace doble clic en cada entrada de la ventana Resultados de la búsqueda 1.  
  
## <a name="see-also"></a>Vea también  
 [Buscar y reemplazar](search-and-replace.md)   
 [Buscar documentos de forma interactiva](search-documents-interactively.md)   
 [Buscar texto con caracteres comodín](search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](search-text-with-regular-expressions.md)  
  
  
