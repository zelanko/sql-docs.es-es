---
title: Destino de ADO NET | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.adonetdest.f1
helpviewer_keywords:
- destinations [Integration Services], ADO.NET
- ADO.NET destination
ms.assetid: cb883990-d875-4d8b-b868-45f9f15ebeae
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ebabe8a6b188c704a45ce022b430156fed17d861
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48165075"
---
# <a name="ado-net-destination"></a>Destino ADO NET
  El destino ADO NET carga datos en una serie de bases de datos compatibles con [!INCLUDE[vstecado](../../includes/vstecado-md.md)]que usan una tabla o vista de base de datos. Tiene la opción de cargar estos datos en una tabla o vista existente, o bien puede crear una nueva tabla y cargar los datos en ella.  
  
 Puede usar el destino de ADO NET para conectarse a [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)]. No se admite la conexión a [!INCLUDE[ssSDS](../../includes/sssds-md.md)] mediante OLE DB. Para obtener más información sobre [!INCLUDE[ssSDS](../../includes/sssds-md.md)], vea [Instrucciones y limitaciones generales de Base de datos SQL de Azure](http://go.microsoft.com/fwlink/?LinkId=248228).  
  
## <a name="troubleshooting-the-ado-net-destination"></a>Solucionar problemas del destino ADO NET  
 Puede registrar las llamadas realizadas por el destino ADO NET a proveedores de datos externos. Puede utilizar esta nueva capacidad de registro para solucionar problemas relacionados con el almacenamiento de datos en orígenes de datos externos que realiza el destino ADO NET. Para registrar las llamadas realizadas por el destino ADO NET a proveedores de datos externos, habilite el registro de paquetes y seleccione el evento **Diagnostic** en el nivel de paquete. Para obtener más información, vea [Herramientas para solucionar problemas con la ejecución de paquetes](../troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
## <a name="configuring-the-ado-net-destination"></a>Configuración del destino ADO NET  
 Este destino usa un administrador de conexiones [!INCLUDE[vstecado](../../includes/vstecado-md.md)] para conectarse a un origen de datos, administrador de conexiones que especifica el proveedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] que se debe usar. Para más información, consulte [ADO.NET Connection Manager](../connection-manager/ado-net-connection-manager.md).  
  
 Un destino ADO NET incluye asignaciones entre columnas de entrada y columnas en el origen de datos de destino. No es preciso que asigne columnas de entrada a todas las columnas de destino. Sin embargo, las propiedades de algunas columnas de destino pueden requerir la asignación de columnas de entrada. De lo contrario, se podrían producir errores. Por ejemplo, si una columna de destino no permite valores NULL, se debe asignar una columna de entrada a esa columna de destino. Además, los tipos de datos de las columnas asignadas deben ser compatibles. Por ejemplo, no es posible asignar una columna de entrada con un tipo de datos de cadena a una columna de destino con un tipo de datos numéricos si el proveedor [!INCLUDE[vstecado](../../includes/vstecado-md.md)] no admite esta asignación.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite insertar texto en las columnas cuyo tipo de datos se haya establecido como imagen. Para obtener más información sobre los tipos de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
> [!NOTE]  
>  El destino ADO NET no permite asignar una columna de entrada cuyo tipo sea DT_DBTIME a una columna de base de datos cuyo tipo sea datetime. Para obtener más información sobre los tipos de datos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , vea [Tipos de datos de Integration Services](integration-services-data-types.md).  
  
 El destino ADO NET tiene una entrada normal y una salida de error.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para obtener más información sobre las propiedades que se pueden establecer en el cuadro de diálogo **Editor de destino ADO NET** , haga clic en uno de los siguientes temas:  
  
-   [Editor de destinos de ADO NET &#40;página Administrador de conexiones&#41;](../ado-net-destination-editor-connection-manager-page.md)  
  
-   [Editor de destinos de ADO NET &#40;página asignaciones&#41;](../ado-net-destination-editor-mappings-page.md)  
  
-   [Editor de destinos de ADO NET &#40;página de salida de Error&#41;](../ado-net-destination-editor-error-output-page.md)  
  
 El cuadro de diálogo **Editor avanzado** indica las propiedades que se pueden establecer mediante programación. Para obtener más información acerca de las propiedades que puede establecer a través del cuadro de diálogo **Editor avanzado** o mediante programación, haga clic en uno de los temas siguientes:  
  
-   [Common Properties](../common-properties.md)  
  
-   [Propiedades personalizadas de ADO NET](ado-net-custom-properties.md)  
  
 Para obtener más información sobre cómo establecer propiedades, vea [Establecer las propiedades de un componente de flujo de datos](set-the-properties-of-a-data-flow-component.md).  
  
  
