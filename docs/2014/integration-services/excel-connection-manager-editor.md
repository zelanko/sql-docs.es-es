---
title: Editor del administrador de conexiones con Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 08dc39cb21eec03a7cbdc5bd56c68212044dd211
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966895"
---
# <a name="excel-connection-manager-editor"></a>Editor de Administrador de conexiones con Excel
  Utilice el cuadro de diálogo **Editor del administrador de conexiones con Excel** para agregar una conexión a un archivo de libro de [!INCLUDE[ofprexcel](../includes/ofprexcel-md.md)] existente o nuevo.  
  
 Para obtener más información acerca del Administrador de conexiones con Excel, vea [Excel Connection Manager](connection-manager/excel-connection-manager.md).  
  
> [!NOTE]  
>  No puede conectar con un archivo de Excel protegido mediante contraseña.  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso del archivo Excel**  
 Escriba la ruta de acceso y el nombre de archivo de un archivo de libro de Excel (.xls) nuevo o existente.  
  
> [!WARNING]  
>  El **Editor de destino de Excel** creará automáticamente el archivo de Excel cuando seleccione una **conexión de Excel** que señale a un archivo nuevo o que no existe y, a continuación, haga clic en **nuevo** en **nombre de la hoja de Excel**.  
  
 **Examinar**  
 Utilice el cuadro de diálogo **abrir** para ir a la carpeta en la que se encuentra el archivo de Excel o donde desea crear el nuevo archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Excel 97-2003|El archivo se ha creado con Excel 97 o una versión posterior.|  
|Excel 3,0|El archivo se creó con Excel 3,0.|  
|Excel 4,0|El archivo se ha creado con Excel 4.0.|  
|Excel 5,0|El archivo se ha creado con Excel 95 (7.0).|  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de errores y mensajes de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Crear bucles entre archivos y tablas de Excel usando un contenedor de bucles Foreach](control-flow/foreach-loop-container.md)  
  
  
