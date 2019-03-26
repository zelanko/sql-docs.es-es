---
title: Administrador de conexiones con Excel | Microsoft Docs
ms.date: 04/02/2018
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.custom: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- files [Integration Services], connections
- connections [Integration Services], Excel
- Excel [Integration Services]
- connection managers [Integration Services], Excel
ms.assetid: 667419f2-74fb-4b50-b963-9197d1368cda
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 67b3b3446cc6890a802e972e9c12a93b3e58c6b0
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/20/2019
ms.locfileid: "58282359"
---
# <a name="excel-connection-manager"></a>Administrador de conexiones con Excel
  Un Administrador de conexiones con Excel permite a un paquete conectarse a un archivo de libro de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Excel. El origen de Excel y el destino de Excel que incluye [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] usan el Administrador de conexiones con Excel.  
 
> [!IMPORTANT]
> Para obtener información detallada sobre cómo conectarse a archivos de Excel y sobre las limitaciones y problemas conocidos a la hora de cargar datos de o a archivos de Excel, vea [Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md).

 Al agregar un Administrador de conexiones con Excel a un paquete, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] crea un Administrador de conexiones que se resuelve como una conexión Excel en el tiempo de ejecución, establece las propiedades del Administrador de conexiones y agrega el Administrador de conexiones a la colección **Conexiones** del paquete.  
  
 La propiedad **ConnectionManagerType** del administrador de conexiones se establece en **EXCEL**.  
  
## <a name="configure-the-excel-connection-manager"></a>Configurar el Administrador de conexiones con Excel  
 Puede configurar el Administrador de conexiones con Excel de las maneras siguientes:  
  
-   Especificar la ruta del archivo de libro de Excel.  
  
-   Especificar la versión de Excel que se usó para crear el archivo.  
  
-   Indicar si la primera fila de las hojas de cálculo o rangos seleccionados contiene nombres de columna.  
  
 Puede establecer propiedades a través del Diseñador de [!INCLUDE[ssIS](../../includes/ssis-md.md)] o mediante programación.  
  
 Para más información sobre las propiedades que puede configurar en el Diseñador [!INCLUDE[ssIS](../../includes/ssis-md.md)] , vea [Editor de Administrador de conexiones con Excel](../../integration-services/connection-manager/excel-connection-manager-editor.md).  
  
 Para obtener información sobre la configuración de un administrador de conexiones mediante programación, vea <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> y [Agregar conexiones mediante programación](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="excel-connection-manager-editor"></a>Editor de Administrador de conexiones con Excel
  Utilice el cuadro de diálogo **Editor del administrador de conexiones con Excel** para agregar una conexión a un archivo de libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] existente o nuevo.  
  
### <a name="options"></a>Opciones  
 **Ruta de acceso del archivo Excel**  
 Escriba la ruta de acceso y el nombre de archivo de un archivo de libro de Excel nuevo o existente.  
   
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para ir a la carpeta donde se encuentra el archivo de Excel o a la ubicación en la que quiere crear el archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="related-tasks"></a>Related Tasks  
[Cargar datos de o a Excel con SQL Server Integration Services (SSIS)](../load-data-to-from-excel-with-ssis.md)  
[Origen de Excel](../data-flow/excel-source.md)  
[Destino de Excel](../data-flow/excel-destination.md)
