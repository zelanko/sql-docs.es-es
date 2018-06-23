---
title: Editor del Administrador de conexiones de Excel | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 27
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 9396c9fe0a04dd7cf8c3f8e408ea22e83dc1c3e5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203993"
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
>  El **Editor de destino de Excel** crea automáticamente el archivo de Excel cuando se selecciona un **conexión con Excel** que apunta a un nuevo/inexistente de archivo y, a continuación, haga clic en **New** para **Nombre de la hoja de Excel**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para ir a la carpeta donde se encuentra el archivo de Excel o a la ubicación en la que quiere crear el archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
|Opción|Descripción|  
|------------|-----------------|  
|Excel 97-2003|El archivo se ha creado con Excel 97 o una versión posterior.|  
|Excel 3.0|Archivo se creó con Excel 3.0.|  
|Excel 4.0|El archivo se ha creado con Excel 4.0.|  
|Excel 5.0|El archivo se ha creado con Excel 95 (7.0).|  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de mensajes y Error de Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Crear bucles entre archivos y tablas de Excel mediante un contenedor de bucles ForEach](control-flow/foreach-loop-container.md)  
  
  