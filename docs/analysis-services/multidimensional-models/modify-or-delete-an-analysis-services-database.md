---
title: Modificar o eliminar una base de datos de Analysis Services | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- databases [Analysis Services], modifying
- removing databases
- deleting databases
- dropping databases
- databases [Analysis Services], deleting
- modifying databases
ms.assetid: e48e3988-c091-4379-aabc-4da62f709a7e
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 65f53460a5a967744e23895b965bda0c9501f8cb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="modify-or-delete-an-analysis-services-database"></a>Modificar o eliminar una base de datos de Analysis Services
  Puede cambiar el nombre y la descripción de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] antes de la implementación en [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] y después de la implementación en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. También puede ajustar parámetros adicionales de una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , de acuerdo al entorno.  
  
> [!NOTE]  
>  No es posible cambiar las propiedades de una base de datos con [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en modo en línea.  
  
## <a name="modifying-databases-using-sql-server-management-studio"></a>Modificar bases de datos mediante SQL Server Management Studio  
 Una vez que se ha implementado una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para cambiar el modo de suplantación que utiliza [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando se conecta a los orígenes de datos que contiene la base de datos. El modo de suplantación permite especificar el contexto de seguridad que usa [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] cuando intenta conectarse a un origen de datos para el procesamiento, la exploración o la obtención de detalles.  
  
## <a name="modifying-databases-using-sql-server-data-tools"></a>Modificar bases de datos mediante las Herramientas de datos de SQL Server  
 Puede utilizar [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] en modo de proyecto para modificar las traducciones del título y la descripción de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que se usa para definir una base de datos. Para más información sobre el uso de traducciones en una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , vea [Escenarios de globalización para Analysis Services](../../analysis-services/globalization-scenarios-for-analysis-services.md).  
  
 También puede establecer los alias y las funciones de agregación asociados con los tipos de cuenta que utilizan los atributos de cuenta de las dimensiones incluidas en la base de datos. Los alias permiten seleccionar la terminología empresarial específica que usa su organización para los tipos de cuenta de un plan de cuentas. Los miembros de un atributo de cuenta utilizan los tipos de cuenta para indicar cómo se agregan medidas a cada miembro utilizando las funciones de agregación especificadas para cada tipo de cuenta que incluye la base de datos. Para más información sobre los atributos de cuenta, vea [Atributos y jerarquías de atributos](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/attributes-and-attribute-hierarchies.md).  
  
## <a name="deleting-databases"></a>eliminar bases de datos  
 Al eliminar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente, se eliminan todos los cubos, dimensiones y modelos de minería de datos de la base de datos. Solo puede eliminar una base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] existente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-delete-an-analysis-services-database"></a>Para eliminar una base de datos de Analysis Services  
  
1.  Conéctese con una instancia de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
2.  En el **Explorador de objetos**, expanda el nodo de la instancia conectada de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y asegúrese de que el objeto que va a eliminar está visible.  
  
3.  Haga clic con el botón derecho en el objeto que quiere eliminar y seleccione **Eliminar**.  
  
4.  En el cuadro de diálogo **Eliminar objeto** , haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Documentar y crear scripts en una base de datos de Analysis Services](../../analysis-services/multidimensional-models/document-and-script-an-analysis-services-database.md)  
  
  
