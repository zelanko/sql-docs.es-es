---
title: Crear un origen de datos (Tutorial de minería de datos básicos) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
caps.latest.revision: 51
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: b86c10563ffae3073b92373eec5e07c18c1c0668
ms.sourcegitcommit: 8c040e5b4e8c7d37ca295679410770a1af4d2e1f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/21/2018
ms.locfileid: "36312593"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>Crear un origen de datos (Tutorial básico de minería de datos)
  A *origen de datos* es una conexión de datos que se guardan y administran en el proyecto e implementa en su [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos. El origen de datos contiene los nombres del servidor y la base de datos donde residen los datos de origen, además de otras propiedades de conexión necesarias.  
  
> [!IMPORTANT]  
>  El nombre de la base de datos es [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Si ya no ha instalado esta base de datos, vea el [bases de datos de ejemplo de Microsoft SQL](http://go.microsoft.com/fwlink/?LinkId=88417) página.  
  
### <a name="to-create-a-data-source"></a>Para crear un origen de datos  
  
1.  En **el Explorador de soluciones**, haga clic en el **orígenes de datos** carpeta y seleccione **nuevo origen de datos**.  
  
2.  En el **éste es el Asistente para orígenes de datos** página, haga clic en **siguiente**.  
  
3.  En el **Seleccione cómo definir la conexión** página, haga clic en **New** para agregar una conexión a la [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] base de datos.  
  
4.  En el **proveedor** lista **Connection Manager**, seleccione **Native OLE DB\SQL Server Native Client 11.0**.  
  
5.  En el **nombre del servidor** cuadro, escriba o seleccione el nombre del servidor en el que instaló [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)].  
  
     Por ejemplo, escriba **localhost** si la base de datos se hospeda en el servidor local.  
  
6.  En el **inicie sesión en el servidor** grupo, seleccione **utilizar autenticación de Windows**.  
  
    > [!IMPORTANT]  
    >  Siempre que sea posible, los implementadores deberían utilizar la autenticación de Windows, ya que proporciona un método de autenticación más seguro que la autenticación de SOL Server. Sin embargo, la autenticación de SQL Server se proporciona por motivos de compatibilidad con versiones anteriores. Para obtener más información acerca de los métodos de autenticación, vea [configuración del motor de base de datos - aprovisionamiento de cuentas](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md).  
  
7.  En el **seleccione o escriba un nombre de base de datos** seleccione [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] y, a continuación, haga clic en **Aceptar**.  
  
8.  Haga clic en **Siguiente**.  
  
9. En el **información de suplantación** página, haga clic en **usar la cuenta de servicio**y, a continuación, haga clic en **siguiente**.  
  
     En el **finalización del Asistente para** página, tenga en cuenta que, de forma predeterminada, el origen de datos se denomina Adventure Works DW 2012.  
  
10. Haga clic en **Finalizar**.  
  
     El nuevo origen de datos, Adventure Works DW 2012, aparece en la **orígenes de datos** carpeta en el Explorador de soluciones.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Creación de datos de una vista del origen &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Proyecto de servicios de creación de un análisis &#40;Tutorial de minería de datos básicos&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un origen de datos &#40;SSAS multidimensional&#41;](../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)   
 [Definir un origen de datos](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [Establecer opciones de suplantación &#40;SSAS - multidimensionales&#41;](../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)  
  
  