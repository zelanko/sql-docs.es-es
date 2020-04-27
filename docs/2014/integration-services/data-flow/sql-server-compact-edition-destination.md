---
title: Destino de SQL Server Compact Edition | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.sqlservercompactdest.f1
helpviewer_keywords:
- destinations [Integration Services], SQL Server Compact
- SQL Server Compact, destination
- inserting data
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: c59157c8d6beccdbb2d3e853cb6e035f9f89f61c
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62901085"
---
# <a name="sql-server-compact-edition-destination"></a>Destino de SQL Server Compact Edition
  El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact escribe datos en bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  En un equipo de 64 bits, necesita ejecutar paquetes que se conecten a los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact en modo de 32 bits. El proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para establecer conexión con orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact solo está disponible en una versión de 32 bits.  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact se configura especificando el nombre de la tabla en la que el destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact inserta los datos. La propiedad personalizada TableName del destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact contiene el nombre de la tabla.  
  
 Este destino usa un administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact para establecer conexión con un origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para obtener más información, vea [Administrador de conexiones con SQL Server Compact Edition](../connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact incluye la propiedad personalizada TableName, que se puede actualizar a través de una expresión de propiedad al cargar el paquete. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas del destino SQL Server Compact Edition](sql-server-compact-edition-destination-custom-properties.md).  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact tiene una entrada y no admite una salida de errores.  
  
## <a name="configuration-of-the-sql-server-compact-edition-destination"></a>Configuración del destino de SQL Server Compact Edition  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas del destino de SQL Server](sql-server-destination-custom-properties.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 Para obtener más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
## <a name="see-also"></a>Consulte también  
 [Flujo de datos](data-flow.md)  
  
  
