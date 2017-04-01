---
title: "Destino de SQL Server Compact Edition | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.sqlservercompactdest.f1"
helpviewer_keywords: 
  - "destinos [Integration Services], SQL Server Compact"
  - "SQL Server Compact, destino"
  - "insertar datos"
ms.assetid: 697742ba-cc14-414d-8187-1845ad0dd99b
caps.latest.revision: 56
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 56
---
# Destino de SQL Server Compact Edition
  El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact escribe datos en bases de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact.  
  
> [!NOTE]  
>  En un equipo de 64 bits, deberá ejecutar paquetes que se conecten a los orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact en modo de 32 bits. Además, el proveedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact que usa [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para establecer conexión con orígenes de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact solo está disponible en una versión de 32 bits.  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact se configura especificando el nombre de la tabla en la que el destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact inserta los datos. La propiedad personalizada TableName del destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact contiene el nombre de la tabla.  
  
 Este destino usa un administrador de conexiones con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact para establecer conexión con un origen de datos, y el administrador de conexiones especifica el proveedor OLE DB que se debe usar. Para obtener más información, vea [Administrador de conexiones con SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md).  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact incluye la propiedad personalizada TableName, que se puede actualizar a través de una expresión de propiedad al cargar el paquete. Para obtener más información, vea [Expresiones de Integration Services &#40;SSIS&#41;](../../integration-services/expressions/integration-services-ssis-expressions.md), [Usar expresiones de propiedad en paquetes](../../integration-services/expressions/use-property-expressions-in-packages.md) y [Propiedades personalizadas del destino SQL Server Compact Edition](../../integration-services/data-flow/sql-server-compact-edition-destination-custom-properties.md).  
  
 El destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Compact tiene una entrada y no admite una salida de errores.  
  
## Configuración del destino de SQL Server Compact Edition  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Propiedades comunes](../Topic/Common%20Properties.md)  
  
-   [Propiedades personalizadas del destino SQL Server](../../integration-services/data-flow/sql-server-destination-custom-properties.md)  
  
## Tareas relacionadas  
 Para obtener más información sobre cómo establecer las propiedades de este componente, vea [Establecer las propiedades de un componente de flujo de datos](../../integration-services/data-flow/set-the-properties-of-a-data-flow-component.md).  
  
## Vea también  
 [Flujo de datos](../../integration-services/data-flow/data-flow.md)  
  
  