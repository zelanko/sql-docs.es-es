---
title: Crear y administrar perspectivas (SSAS Tabular) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 2af9c28c5c63edc873ef549527333b4ba353cb08
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="create-and-manage-perspectives-ssas-tabular"></a>Crear y administrar perspectivas (SSAS tabular)
  Las perspectivas definen subconjuntos visibles de un modelo que ofrecen puntos de vista centrados, específicos del negocio o específicos de la aplicación del modelo. Las tareas de este tema explican cómo crear y administrar perspectivas mediante el cuadro de diálogo **Perspectivas** del diseñador de modelos.  
  
 En este tema se incluyen las tareas siguientes:  
  
-   [Para agregar una perspectiva](#bkmk_add)  
  
-   [Para editar una perspectiva](#bkmk_edit)  
  
-   [Para cambiar el nombre de una perspectiva](#bkmk_rename)  
  
-   [Para eliminar una perspectiva](#bkmk_delete)  
  
-   [Para copiar una perspectiva](#bkmk_copy)  
  
## <a name="tasks"></a>Tareas  
 Para crear las perspectivas, use el cuadro de diálogo **Perspectivas** , donde podrá agregar, editar, eliminar, copiar y ver las perspectivas. Para ver el cuadro de diálogo **Perspectivas** , en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], haga clic en el menú **Modelo** y en **Perspectivas**.  
  
###  <a name="bkmk_add"></a> Para agregar una perspectiva  
  
-   Para agregar una perspectiva nueva, haga clic en **Nueva perspectiva**. A continuación puede activar y desactivar los objetos de campo que se van a incluir, así como especificar un nombre para la nueva perspectiva.  
  
     Si crea una perspectiva vacía con todos los objetos de campo, un usuario que use esta perspectiva verá una lista de campos vacía. Las perspectivas deben contener al menos una tabla y una columna.  
  
###  <a name="bkmk_edit"></a> Para editar una perspectiva  
  
-   Para modificar una perspectiva, active y desactive los campos en la columna de la perspectiva, lo que agrega y quita objetos de campo de la perspectiva.  
  
###  <a name="bkmk_rename"></a> Para cambiar el nombre de una perspectiva  
  
-   Al mantener el mouse sobre el encabezado de columna de una perspectiva (el nombre de la perspectiva), aparece el botón **Cambiar nombre** . Para cambiar el nombre de la perspectiva, haga clic en **Cambiar nombre**y, a continuación, escriba un nuevo nombre o edite el nombre existente.  
  
###  <a name="bkmk_delete"></a> Para eliminar una perspectiva  
  
-   Al mantener el mouse sobre el encabezado de columna de una perspectiva (el nombre de la perspectiva), aparece el botón **Eliminar** . Para eliminar la perspectiva, haga clic en el botón **Eliminar** y, a continuación, haga clic en **Sí** en la ventana de confirmación.  
  
###  <a name="bkmk_copy"></a> Para copiar una perspectiva  
  
-   Al mantener el mouse sobre el encabezado de columna de una perspectiva, aparece el botón **Copiar** . Para crear una copia de esa perspectiva, haga clic en el botón **Copiar** . Se agregará una copia de la perspectiva seleccionada como una perspectiva nueva a la derecha de las perspectivas existentes. La nueva perspectiva hereda el nombre de la perspectiva copiada y se anexa una anotación *-Copia* al final del nombre. Por ejemplo, si se crea una copia de la perspectiva *Ventas* , la nueva perspectiva se llama *Ventas – Copiar*.  
  
## <a name="see-also"></a>Vea también  
 [Perspectivas &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Jerarquías &#40;SSAS tabular&#41;](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
