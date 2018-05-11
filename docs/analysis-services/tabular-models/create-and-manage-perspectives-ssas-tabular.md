---
title: Crear y administrar perspectivas | Documentos de Microsoft
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d98d2498eee3f1ac9e847828dc41888c4fd0c963
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
---
# <a name="create-and-manage-perspectives"></a>Crear y administrar perspectivas 
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  Las perspectivas definen subconjuntos visibles de un modelo que ofrecen puntos de vista centrados, específicos del negocio o específicos de la aplicación del modelo. Las tareas de este tema explican cómo crear y administrar perspectivas mediante el cuadro de diálogo **Perspectivas** del diseñador de modelos.  
  
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
 [Perspectivas](../../analysis-services/tabular-models/perspectives-ssas-tabular.md)   
 [Jerarquías](../../analysis-services/tabular-models/hierarchies-ssas-tabular.md)  
  
  
