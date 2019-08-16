---
title: Crear un origen de datos (tutorial básico de minería de datos) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: d7107c32-69ed-49a8-9b6e-32753eebf42c
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 3f85320a99c901a2fd71c9048750825569559099
ms.sourcegitcommit: f5807ced6df55dfa78ccf402217551a7a3b44764
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/15/2019
ms.locfileid: "69494024"
---
# <a name="creating-a-data-source-basic-data-mining-tutorial"></a>Crear un origen de datos (Tutorial básico de minería de datos)
  Un *origen de datos* es una conexión de datos que se guarda y administra en el proyecto y se [!INCLUDE[msCoName](../includes/msconame-md.md)] implementa en la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] base de datos. El origen de datos contiene los nombres del servidor y la base de datos donde residen los datos de origen, además de otras propiedades de conexión necesarias.  
  
> [!IMPORTANT]  
>  El nombre de la base de datos es [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]. Si aún no ha instalado esta base de datos, vea la página bases de datos de [ejemplo de Microsoft SQL](https://go.microsoft.com/fwlink/?LinkId=88417) .  
  
### <a name="to-create-a-data-source"></a>Para crear un origen de datos  
  
1.  En **Explorador de soluciones**, haga clic con el botón secundario en la carpeta **orígenes de datos** y seleccione **nuevo origen de datos**.  
  
2.  En la página **éste es el Asistente para orígenes de datos** , haga clic en **siguiente**.  
  
3.  En la página **seleccionar cómo definir la conexión** , haga clic en **nuevo** para agregar una conexión a [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] la base de datos.  
  
4.  En la lista **proveedor** del **Administrador de conexiones**, seleccione **OLE DB nativo\sql Server Native Client 11,0**.  
  
5.  En el cuadro **nombre del servidor** , escriba o seleccione el nombre del servidor en el que ha [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)]instalado.  
  
     Por ejemplo, escriba **localhost** si la base de datos está hospedada en el servidor local.  
  
6.  En el grupo **iniciar sesión en el servidor** , seleccione **usar autenticación de Windows**.  
  
    > [!IMPORTANT]  
    >  Siempre que sea posible, los implementadores deberían utilizar la autenticación de Windows, ya que proporciona un método de autenticación más seguro que la autenticación de SOL Server. Sin embargo, la autenticación de SQL Server se proporciona por motivos de compatibilidad con versiones anteriores. Para obtener más información acerca de los métodos de autenticación, consulte [configuración de motor de base de datos: aprovisionamiento de cuentas](../../2014/sql-server/install/database-engine-configuration-account-provisioning.md).  
  
7.  En la lista **Seleccione o escriba un nombre de base** de [!INCLUDE[ssSampleDBDWobject](../includes/sssampledbdwobject-md.md)] datos, seleccione y, a continuación, haga clic en **Aceptar**.  
  
8.  Haga clic en **Next**.  
  
9. En la página **información** de suplantación, haga clic en **usar la cuenta de servicio**y, a continuación, haga clic en **siguiente**.  
  
     En la página **finalización del asistente** , observe que, de forma predeterminada, el origen de datos se denomina Adventure Works DW 2012.  
  
10. Haga clic en **Finalizar**  
  
     El nuevo origen de datos, Adventure Works DW 2012, aparece en la carpeta **orígenes de datos** de explorador de soluciones.  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Crear una vista &#40;del origen de datos tutorial básico de minería de datos&#41;](../../2014/tutorials/creating-a-data-source-view-basic-data-mining-tutorial.md)  
  
## <a name="previous-task-in-lesson"></a>Tarea anterior de la lección  
 [Creación de un tutorial &#40;básico de minería de datos de Analysis Services Project&#41;](../../2014/tutorials/creating-an-analysis-services-project-basic-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear un origen de datos &#40;SSAS multidimensional&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional)   
 [Definir un origen de datos](../analysis-services/lesson-1-2-defining-a-data-source.md)   
 [Establezca las opciones de suplantación &#40;SSAS - multidimensional&#41;](https://docs.microsoft.com/analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional)  
  
  
