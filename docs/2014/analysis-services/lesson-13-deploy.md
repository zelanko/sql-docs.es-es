---
title: 'Lección 14: Implementar | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96ffa6445d46f1e68efa907330d0945a499bf3b2
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66079138"
---
# <a name="lesson-14-deploy"></a>Lección 14: Implementar
  En esta lección, configurará propiedades de implementación, especificará una instancia del servidor de implementación de Analysis Services que se ejecute en modo tabular y asignará un nombre al modelo que va a implementar. A continuación, implementará el modelo en esa instancia. Una vez implementado, los usuarios podrán conectarse al modelo mediante una aplicación cliente de informes. Para obtener más información, vea [Implementación de soluciones de modelos tabulares &#40;SSAS tabular&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Tiempo estimado para completar esta lección: **5 minutos**  
  
## <a name="prerequisites"></a>Requisitos previos  
 Este tema es parte de un tutorial de creación de modelos tabulares, que se debe completar en orden. Antes de realizar las tareas en esta lección, debe haber completado la lección anterior: [Lección 13: Analizar en Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implementar el modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propiedades de implementación  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], en **Explorador de soluciones**, haga clic con el botón derecho en **Modelo tabular de ventas por Internet de Adventure Works** y, en el menú contextual, haga clic en **Propiedades**.  
  
2.  En el cuadro de diálogo **Páginas de propiedades del modelo tabular de ventas por Internet de AW** , bajo **Servidor de implementación**, en la propiedad **Server** , escriba el nombre de una instancia de Analysis Services que se ejecute en modo Tabular. Esta será la instancia en la que se implementará el modelo.  
  
    > [!IMPORTANT]  
    >  Debe tener permisos de administrador en una instancia de Analysis Services remota para poder implementarlo.  
  
3.  Compruebe el **el modo de consulta** propiedad está establecida en **In-Memory**.  
  
    > [!NOTE]  
    >  El modelo creado mediante este tutorial no admite el modo DirectQuery.  
  
4.  En el **base de datos** propiedad, tipo `Adventure Works Internet Sales Model`.  
  
5.  En el **cubo** propiedad de nombre, escriba `Adventure Works Internet Sales Model`.  
  
6.  Compruebe las opciones seleccionadas y, después, haga clic en **Aceptar**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implementar el modelo tabular Ventas por Internet de Adventure Works  
  
1.  En [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], haga clic en el menú **Generar** y, después, haga clic en **Implementar modelo tabular de ventas por Internet de AW**.  
  
     Aparece el cuadro de diálogo Implementar en el que se muestra el estado de implementación de los metadatos y las tablas incluidas en el modelo.  
  
## <a name="conclusion"></a>Conclusión  
 ¡Enhorabuena! Ha terminado de crear e implementar su primer modelo tabular de Analysis Services. Este tutorial le ha guiado por las tareas más comunes para crear un modelo tabular. Ahora que su modelo Ventas por Internet de Adventure Works está implementado, puede utilizar el SQL Server Management Studio para administrarlo, crear scripts de proceso y realizar un plan de copia de seguridad. Los usuarios pueden conectarse al modelo mediante una aplicación cliente de informes como Microsoft Excel o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Recursos adicionales  
 Para obtener más información sobre las propiedades de modelo tabular que admiten informes de [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], vea [Propiedades de informes de Power View &#40;SSAS tabular&#41;](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>Vea también  
 [Modo DirectQuery &#40;SSAS tabular&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar las propiedades predeterminadas de modelado de datos y de implementación &#40;SSAS tabular&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Bases de datos de modelo tabular &#40;SSAS tabular&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
