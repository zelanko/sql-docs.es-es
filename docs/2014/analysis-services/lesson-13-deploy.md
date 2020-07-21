---
title: 'Lección 14: implementar | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8b930734fa70578d10e107bc3d1e8d865f9e7e2d
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84543537"
---
# <a name="lesson-14-deploy"></a>Lección 14: Implementar
  En esta lección, configurará propiedades de implementación, especificará una instancia del servidor de implementación de Analysis Services que se ejecute en modo tabular y asignará un nombre al modelo que va a implementar. A continuación, implementará el modelo en esa instancia. Una vez implementado, los usuarios podrán conectarse al modelo mediante una aplicación cliente de informes. Para obtener más información, vea [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden. Antes de realizar las tareas de esta lección, debe haber completado la lección anterior: [Lección 13: Analizar en Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implementar el modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar las propiedades de implementación, siga estos pasos:  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en **Explorador de soluciones**, haga clic con el botón derecho en **Modelo tabular de ventas por Internet de Adventure Works** y, en el menú contextual, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Páginas de propiedades del modelo tabular de ventas por Internet de AW** , bajo **Servidor de implementación**, en la propiedad **Server** , escriba el nombre de una instancia de Analysis Services que se ejecute en modo Tabular. Esta será la instancia en la que se implementará el modelo.  
  
    > [!IMPORTANT]  
    >  Debe tener permisos de administrador en una instancia de Analysis Services remota para poder implementarlo.  
  
3.  Compruebe que la propiedad **modo de consulta** está establecida en **in-memory**.  
  
    > [!NOTE]  
    >  El modelo creado mediante este tutorial no admite el modo DirectQuery.  
  
4.  En la propiedad **Database** , escriba `Adventure Works Internet Sales Model` .  
  
5.  En la propiedad nombre del **cubo** , escriba `Adventure Works Internet Sales Model` .  
  
6.  Compruebe sus selecciones y, a continuación, haga clic en **Aceptar**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implementar el modelo tabular Ventas por Internet de Adventure Works  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Generar** y, después, haga clic en **Implementar modelo tabular de ventas por Internet de AW**.  
  
     Aparece el cuadro de diálogo Implementar en el que se muestra el estado de implementación de los metadatos y las tablas incluidas en el modelo.  
  
## <a name="conclusion"></a>Conclusión  
 ¡Enhorabuena! Ha terminado de crear e implementar su primer modelo tabular de Analysis Services. Este tutorial le ha ayudado a completar las tareas más comunes en la creación de un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios pueden conectarse al modelo mediante una aplicación cliente de informes como Microsoft Excel o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Recursos adicionales  
 Para obtener más información sobre las propiedades de modelo tabular que admiten informes de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], vea [Propiedades de informes de Power View &#40;SSAS tabular&#41;](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>Consulte también  
 [Modo DirectQuery &#40;&#41;tabular de SSAS](tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Bases de datos de modelo tabular &#40;SSAS tabular&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
