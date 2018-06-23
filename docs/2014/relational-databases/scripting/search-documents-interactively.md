---
title: Buscar documentos de forma interactiva | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
caps.latest.revision: 21
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 0957ca100cfc9e4f37e1255416a91def14ab037a
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201347"
---
# <a name="search-documents-interactively"></a>Buscar documentos de forma interactiva
  Mediante el cuadro de diálogo **Buscar y reemplazar** , puede buscar en uno o más archivos o ventanas abiertos y desplazarse por las coincidencias una a una. Esta técnica permite revisar cada coincidencia individual en el contexto en que se encuentra. El cuadro de diálogo **Buscar y reemplazar** también ofrece la opción de realizar operaciones de búsqueda masiva y revisión de coincidencias en formato de informe.  
  
### <a name="to-search-all-open-documents"></a>Para buscar en todos los documentos abiertos  
  
1.  Abra los elementos en los que desea buscar.  
  
2.  En el menú **Editar** , elija **Buscar y reemplazar** y, después, haga clic en **Búsqueda rápida**.  
  
3.  En el cuadro de texto **Buscar y reemplazar** , escriba el texto que desea buscar.  
  
4.  En la lista **Buscar en** , seleccione **Todos los documentos abiertos**.  
  
    > [!NOTE]  
    >  Cuando se selecciona **Todos los documentos abiertos** , puede que no se busque en algunos archivos abiertos. Solo se incluyen en las búsquedas aquellos archivos abiertos actualmente en una vista de texto, como la vista Código. Los archivos abiertos en la vista del diseñador no se incluyen en las búsquedas.  
  
5.  Seleccione opciones de búsqueda adicionales para aumentar la precisión de la misma.  
  
6.  Haga clic en **Buscar siguiente** para iniciar la búsqueda y siga haciendo clic en **Buscar siguiente** hasta que haya buscado en el último archivo.  
  
 Cuando la búsqueda pasa el comienzo o el final del documento, aparece un mensaje en la barra de estado. Cuando la búsqueda alcanza el punto de inicio, aparece un cuadro de mensaje.  
  
#### <a name="to-replace-in-all-active-files-interactively"></a>Para reemplazar en todos los archivos activos de forma interactiva  
  
1.  En el menú **Editar** , elija **Buscar y reemplazar**y, después, haga clic en **Reemplazo rápido**.  
  
2.  En el cuadro **Buscar** , escriba el texto que desea buscar.  
  
3.  En el cuadro **Reemplazar con** , escriba el texto que reemplazará al texto de la búsqueda.  
  
4.  En la lista **Buscar en** , seleccione **Todos los documentos abiertos**.  
  
5.  Haga clic en **Reemplazar**y siga haciendo clic en **Reemplazar** hasta que haya reemplazado la última coincidencia del última archivo. Haga clic en **Buscar siguiente** para omitir una coincidencia que no desea reemplazar.  
  
     -o bien-  
  
     Elija **Reemplazar todo** para reemplazar todas las coincidencias. Aparecerá un cuadro de mensaje indicando el número total de reemplazos.  
  
 El comando **Reemplazar todo** reemplaza todas las coincidencias de la búsqueda, incluidas aquellas que se han omitido mediante el botón **Buscar siguiente** . Para cancelar **Reemplazar todo**, haga clic en **Deshacer** en el menú **Editar** antes de cerrar cualquiera de los archivos.  
  
## <a name="see-also"></a>Vea también  
 [Buscar en un documento activo de forma incremental](search-an-active-document-incrementally.md)   
 [Buscar y reemplazar](search-and-replace.md)   
 [Buscar en documentos mediante las listas de resultados](search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](search-text-with-regular-expressions.md)  
  
  