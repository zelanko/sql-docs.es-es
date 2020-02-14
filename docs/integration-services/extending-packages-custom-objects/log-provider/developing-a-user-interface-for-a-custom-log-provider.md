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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: fccc03acb846fe1fe7db12d339c633b7d4c7e306
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/01/2020
ms.locfileid: "71297140"
---
# <a name="developing-a-user-interface-for-a-custom-log-provider"></a>Desarrollar una interfaz de usuario para un proveedor de registro personalizado

[!INCLUDE[ssis-appliesto](../../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Muchos proveedores de registro de [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] tienen una interfaz de usuario personalizada que implementa <xref:Microsoft.SqlServer.Dts.Runtime.Design.IDtsLogProviderUI> y reemplaza el cuadro de texto **Configuración** en el cuadro de diálogo **Configurar registros de SSIS** por una lista desplegable filtrada de administradores de conexiones disponibles. Sin embargo, las interfaces de usuario personalizadas para los proveedores de registro personalizados no se implementan en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
## <a name="see-also"></a>Consulte también  
 [Crear un proveedor de registro personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/creating-a-custom-log-provider.md)   
 [Codificar un proveedor de registro personalizado](../../../integration-services/extending-packages-custom-objects/log-provider/coding-a-custom-log-provider.md)  
  
  
