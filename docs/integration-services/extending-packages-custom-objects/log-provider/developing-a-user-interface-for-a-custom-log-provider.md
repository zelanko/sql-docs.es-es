---
title: Desarrollar una interfaz de usuario para un proveedor de registro personalizado | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: reference
helpviewer_keywords:
- custom user interface [Integration Services], custom log providers
- custom log providers [Integration Services], developing custom user interface
ms.assetid: 6fd2d269-d87a-4134-82a1-40a09b3b5453
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ea7010ed5c9a0399023c455fff2fc324297a0d0f
ms.sourcegitcommit: fd71d04a9d30a9927cbfff645750ac9d5d5e5ee7
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/16/2019
ms.locfileid: "65724519"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>Desarrollar una interfaz de usuario para un proveedor de registro personalizado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Muchos proveedores de registro de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tienen una interfaz de usuario personalizada que implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> y reemplaza el cuadro de texto **Configuración** en el cuadro de diálogo **Configurar registros de SSIS** por una lista desplegable filtrada de administradores de conexiones disponibles. Sin embargo, las interfaces de usuario personalizadas para los proveedores de registro personalizados no se implementan en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Crear un proveedor de registro personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [Codificar un proveedor de registro personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
