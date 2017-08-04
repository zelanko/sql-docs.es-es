---
title: Editor del Administrador de conexiones de Excel | Documentos de Microsoft
ms.custom:
- SQL2016_New_Updated
ms.date: 03/02/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.excelconnection.f1
helpviewer_keywords:
- Excel Connection Manager Editor
ms.assetid: 7ff097e4-cafb-4885-a898-05b2a46628c1
caps.latest.revision: 32
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 3c4060736f824becd05fecceba0b162b45f0fed4
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="excel-connection-manager-editor"></a>Editor de Administrador de conexiones con Excel
  Utilice el cuadro de diálogo **Editor del administrador de conexiones con Excel** para agregar una conexión a un archivo de libro de [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] existente o nuevo.  
  
 Para obtener más información acerca del Administrador de conexiones con Excel, vea [Excel Connection Manager](../../integration-services/connection-manager/excel-connection-manager.md).  
  
## <a name="options"></a>Opciones  
 **Ruta de acceso del archivo Excel**  
 Escriba la ruta de acceso y el nombre de archivo de un archivo de libro de Excel (.xls) nuevo o existente.  
  
> [!NOTE]  
>  No puede conectar con un archivo de Excel protegido mediante contraseña.  
  
> [!WARNING]  
>  El **Editor de destino de Excel** creará automáticamente el archivo de Excel cuando seleccione una **Conexión de Excel** que señale a un archivo nuevo o inexistente y haga clic en **Nuevo** en **Nombre de la hoja de Excel**.  
  
 **Examinar**  
 Use el cuadro de diálogo **Abrir** para ir a la carpeta donde se encuentra el archivo de Excel o a la ubicación en la que quiere crear el archivo.  
  
 **Versión de Excel**  
 Especifique la versión de Microsoft Excel utilizada para crear el archivo.  
  
 **La primera fila tiene nombres de columna**  
 Especifique si la primera fila de datos de la hoja seleccionada contiene nombres de columna. El valor predeterminado de esta opción es **True**.  
  
## <a name="providers-and-drivers-for-microsoft-excel-and-access-file"></a>Proveedores y controladores de archivo de Microsoft Excel y Access  
 Tendrá que descargar los proveedores y controladores OLE DB para los archivos de Microsoft Office si no están instalados. Las versiones posteriores del proveedor pueden abrir archivos creados con versiones anteriores de Excel.  
  
 Si el equipo tiene una versión de Office de 32 bits, tendrá que instalar la versión de 32 bits de los controladores, y también debe asegurarse de que ejecuta el asistente o el paquete de Integration Services que se crea en el modo de 32 bits.  
  
|Versión de Microsoft Office|Descargar|  
|------------------------------|--------------|  
|2007|[Controlador de 2007 Office System: componentes de conectividad de datos](https://www.microsoft.com/download/details.aspx?id=23734)|  
|2010|[Microsoft Access 2010 Runtime](https://www.microsoft.com/download/details.aspx?id=10910)|  
|2013|[Microsoft Access 2013 Runtime](http://www.microsoft.com/download/details.aspx?id=39358)|  
|2016|[Microsoft Access 2016 Runtime](https://www.microsoft.com/download/details.aspx?id=50040)|
  
## <a name="see-also"></a>Vea también  
 [Referencia de errores y mensajes de Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Bucle a través de Excel, archivos y tablas mediante el uso de un contenedor de bucles Foreach](../../integration-services/control-flow/loop-through-excel-files-and-tables-by-using-a-foreach-loop-container.md)  
  
  
