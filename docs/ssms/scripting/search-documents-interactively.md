---
title: Buscar documentos de forma interactiva | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.technology: scripting
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- interactive searches [SQL Server Management Studio]
- searches [SQL Server Management Studio], interactive
- Query Editor [SQL Server Management Studio], interactive search
ms.assetid: dae65ac5-67af-45c6-a6e0-952fea26d680
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 67e8e90d8ca45afd827ca44a4fa87ced24184505
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/16/2019
ms.locfileid: "68264194"
---
# <a name="search-documents-interactively"></a>Buscar documentos de forma interactiva
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
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
  
     -O bien-  
  
     Elija **Reemplazar todo** para reemplazar todas las coincidencias. Aparecerá un cuadro de mensaje indicando el número total de reemplazos.  
  
 El comando **Reemplazar todo** reemplaza todas las coincidencias de la búsqueda, incluidas aquellas que se han omitido mediante el botón **Buscar siguiente** . Para cancelar **Reemplazar todo**, haga clic en **Deshacer** en el menú **Editar** antes de cerrar cualquiera de los archivos.  
  
## <a name="see-also"></a>Consulte también  
 [Buscar en un documento activo de forma incremental](../../relational-databases/scripting/search-an-active-document-incrementally.md)   
 [Buscar y reemplazar](../../relational-databases/scripting/search-and-replace.md)   
 [Buscar en documentos mediante las listas de resultados](../../relational-databases/scripting/search-documents-using-results-lists.md)   
 [Buscar texto con caracteres comodín](../../relational-databases/scripting/search-text-with-wildcards.md)   
 [Buscar texto mediante expresiones regulares](../../relational-databases/scripting/search-text-with-regular-expressions.md)  
  
  
