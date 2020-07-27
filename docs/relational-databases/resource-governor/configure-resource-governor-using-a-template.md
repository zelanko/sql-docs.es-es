---
title: Configuración del regulador de recursos utilizando una plantilla | Microsoft Docs
description: Obtenga información sobre cómo configurar Resource Governor mediante una plantilla proporcionada en SQL Server Management Studio. Debe tener el permiso CONTROL SERVER.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- Resource Governor, templates
ms.assetid: f342dec2-d1d6-483e-b44e-98eb7d168b5e
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: b815330ad5088ca449ab3b73f540b3ec2e521629
ms.sourcegitcommit: 9470c4d1fc8d2d9d08525c4f811282999d765e6e
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2020
ms.locfileid: "86458240"
---
# <a name="configure-resource-governor-using-a-template"></a>Configurar el regulador de recursos utilizando una plantilla
[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]
  Puede configurar el regulador de recursos utilizando una plantilla que se proporciona en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
-   **Antes de empezar:**  [Permisos](#Permissions)  
  
-   **Para crear un grupo de cargas de trabajo mediante:** [una plantilla](#ConfRGTemplate)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
 Siga los pasos que se detallan a continuación para abrir y modificar una plantilla que crea un grupo de recursos de servidor y un grupo de cargas de trabajo para el grupo de recursos. Además, esta plantilla le permite crear una función clasificadora definida por el usuario que enruta las nuevas conexiones al grupo predeterminado o al grupo de cargas de trabajo que está creando.  
  
###  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] del regulador de recursos de la plantilla requieren el permiso CONTROL SERVER.  
  
##  <a name="configure-resource-governor-using-a-template"></a><a name="ConfRGTemplate"></a> Configurar el regulador de recursos utilizando una plantilla  
 **Para configurar el regulador de recursos utilizando una plantilla en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]**  
  
1.  En [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], en el menú **Ver** , haga clic en el **Explorador de plantillas**.  
  
2.  En **Explorador de plantillas**, expanda **Regulador de recursos**y, luego, haga doble clic en **Configurar regulador de recursos**.  
  
3.  En **Conectar al motor de base de datos**, escriba la información necesaria y, a continuación, haga clic en **Aceptar**. La plantilla Configure Resource Governor.sql se proporciona junto con el Editor de consultas. Utilice esta plantilla para crear y configurar un grupo de recursos de servidor, un grupo de cargas de trabajo y una función clasificadora.  
  
4.  Para modificar los valores de la plantilla, pulse CTRL+MAYÚS+M. En el cuadro de diálogo **Especificar valores para parámetros de plantilla** , escriba los valores que desea utilizar.  
  
5.  Para guardar los cambios que realice en la plantilla, haga clic en **Aceptar**.  
  
6.  Para ejecutar la consulta, haga clic en **Ejecutar**.  

## <a name="see-also"></a>Consulte también  
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
  
  
