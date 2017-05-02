---
title: "Configuración del regulador de recursos utilizando una plantilla | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
caps.latest.revision: 15
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 37a30ac49e0b7af05e0c7fb8e2ac1a32824186f6
ms.lasthandoff: 04/11/2017

---
# <a name="configure-resource-governor-using-a-template"></a>Configurar el regulador de recursos utilizando una plantilla
  Puede configurar el regulador de recursos utilizando una plantilla que se proporciona en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Before you begin:**  [Permissions](#Permissions)  
  
-   **To create a workload group, using:**  [a template](#ConfRGTemplate)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
 Siga los pasos que se detallan a continuación para abrir y modificar una plantilla que crea un grupo de recursos de servidor y un grupo de cargas de trabajo para el grupo de recursos. Además, esta plantilla le permite crear una función clasificadora definida por el usuario que enruta las nuevas conexiones al grupo predeterminado o al grupo de cargas de trabajo que está creando.  
  
###  <a name="Permissions"></a> Permisos  
 Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] del regulador de recursos de la plantilla requieren el permiso CONTROL SERVER.  
  
##  <a name="ConfRGTemplate"></a> Configurar el regulador de recursos utilizando una plantilla  
 **Para configurar el regulador de recursos utilizando una plantilla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  En **Explorador de plantillas**, expanda **Regulador de recursos**y, luego, haga doble clic en **Configurar regulador de recursos**.  
  
3.  En **Conectar al motor de base de datos**, escriba la información necesaria y, a continuación, haga clic en **Aceptar**. La plantilla Configure Resource Governor.sql se proporciona junto con el Editor de consultas. Utilice esta plantilla para crear y configurar un grupo de recursos de servidor, un grupo de cargas de trabajo y una función clasificadora.  
  
4.  Para modificar los valores de la plantilla, pulse CTRL+MAYÚS+M. En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , escriba los valores que desea utilizar.  
  
5.  Para guardar los cambios que realice en la plantilla, haga clic en **Aceptar**.  
  
6.  Para ejecutar la consulta, haga clic en **Ejecutar**.  
  
## <a name="see-also"></a>Vea también  
 [Regulador de recursos](../../relational-databases/resource-governor/resource-governor.md)   
 [Habilitar el regulador de recursos](../../relational-databases/resource-governor/enable-resource-governor.md)   
 [Grupo de recursos de servidor del regulador de recursos](../../relational-databases/resource-governor/resource-governor-resource-pool.md)   
 [Grupos de cargas de trabajo del regulador de recursos](../../relational-databases/resource-governor/resource-governor-workload-group.md)   
 [Función clasificadora del regulador de recursos](../../relational-databases/resource-governor/resource-governor-classifier-function.md)   
 [Ver las propiedades del regulador de recursos](../../relational-databases/resource-governor/view-resource-governor-properties.md)   
 [CREATE RESOURCE POOL &#40;Transact-SQL&#41;](../../t-sql/statements/create-resource-pool-transact-sql.md)   
 [CREATE WORKLOAD GROUP &#40;Transact-SQL&#41;](../../t-sql/statements/create-workload-group-transact-sql.md)   
 [CREATE FUNCTION &#40;Transact-SQL&#41;](../../t-sql/statements/create-function-transact-sql.md)   
 [ALTER RESOURCE GOVERNOR &#40;Transact-SQL&#41;](../../t-sql/statements/alter-resource-governor-transact-sql.md)  
  
  
