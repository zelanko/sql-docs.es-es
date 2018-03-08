---
title: Crear y administrar perspectivas | Documentos de Microsoft
ms.custom: 
ms.date: 02/22/2018
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.asvs.bidtoolset.perspectivedb.f1
ms.assetid: 2a411c2b-2820-4086-ad7f-ce6a941fefc7
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5149052156082507c6c970512ab7db0194209ab5
ms.sourcegitcommit: d8ab09ad99e9ec30875076acee2ed303d61049b7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/23/2018
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
  
  
