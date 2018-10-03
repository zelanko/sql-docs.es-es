---
title: Administrador de conexiones de Excel | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 403fe52b67756a32a4229df83fdf9fa56a0bb8a3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48069495"
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
>  El **Editor de destino de Excel** crea automáticamente el archivo de Excel cuando se selecciona un **conexión de Excel** que apunta a un nuevo o inexistente de archivo y, a continuación, haga clic en **New** para **Nombre de la hoja de Excel**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para ir a la carpeta donde se encuentra el archivo de Excel o a la ubicación en la que quiere crear el archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Excel 97-2003|El archivo se ha creado con Excel 97 o una versión posterior.|  
|Excel 3.0|Archivo creado con Excel 3.0.|  
|Excel 4.0|El archivo se ha creado con Excel 4.0.|  
|Excel 5.0|El archivo se ha creado con Excel 95 (7.0).|  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles ForEach](control-flow/foreach-loop-container.md)  
  
  
