---
title: Organizador de configuraciones de paquete | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.packageconfigurationorganizer.f1
helpviewer_keywords:
- Package Configurations Organizer dialog box
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: d5313118f7949818d341a47744a69cf13c43dbc9
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2019
ms.locfileid: "66056966"
---
# <a name="package-configurations-organizer"></a>Organizador de configuraciones de paquetes
  Utilice el cuadro de diálogo **Organizador de configuraciones de paquetes** para habilitar las configuraciones de paquetes, ver una lista de configuraciones para el paquete actual y especificar el orden de preferencia en el que se deben cargar las configuraciones.  
  
> [!NOTE]  
>  Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](packages/deploy-integration-services-ssis-projects-and-packages.md).  
  
 Si varias configuraciones actualizan la misma propiedad, los valores de las configuraciones que aparezcan más abajo en la lista reemplazarán los valores de aquéllas que ocupen un lugar superior en la lista. El último valor cargado en la propiedad es el valor que se usa cuando se ejecuta el paquete. Asimismo, si el paquete utiliza una combinación de configuración directa, como un archivo de configuración XML, y configuración indirecta, como una variable de entorno, la configuración indirecta que señala a la ubicación de la configuración directa debe ocupar un lugar superior en la lista.  
  
> [!NOTE]  
>  Cuando las configuraciones de paquetes se cargan en el orden preferido, se cargan de arriba a abajo, según la lista que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes** . Sin embargo, en tiempo de ejecución, las configuraciones de paquetes podrían no cargarse en el orden preferido. Concretamente, las configuraciones de paquetes principales se cargan después de las configuraciones de otros tipos.  
  
 Las configuraciones de paquetes actualizan los valores de las propiedades de los objetos de paquete en tiempo de ejecución. Cuando se carga un paquete, los valores de las configuraciones reemplazan los valores establecidos cuando se desarrolló el paquete. [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] admite distintos tipos de configuración. Por ejemplo, se puede utilizar un archivo XML que contenga múltiples configuraciones o una variable de entorno que contenga una única configuración. Para obtener más información, vea [Package Configurations](../../2014/integration-services/package-configurations.md).  
  
## <a name="options"></a>Opciones  
 **Habilitar configuraciones de paquetes**  
 Seleccione esta opción para utilizar las configuraciones incluidas con el paquete.  
  
 **Nombre de la configuración**  
 Presenta el nombre de la configuración.  
  
 **Tipo de configuración**  
 Presenta el tipo de la ubicación donde se almacenan las configuraciones.  
  
 **Cadena de configuración**  
 Presenta la ubicación donde se almacenan los valores de configuración. La ubicación puede ser la ruta de acceso a un archivo, el nombre de una variable de entorno, el nombre de una variable de paquete principal, una clave del Registro o el nombre de una tabla de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 **Objeto de destino**  
 Muestra el nombre del objeto que la configuración actualiza. Si la configuración se encuentra en un archivo de configuración XML o una tabla de SQL Server, la columna aparece en blanco, ya que la configuración puede incluir varios objetos.  
  
 **Propiedad de destino**  
 Presenta el nombre de la propiedad modificada por la configuración. La columna está en blanco si el tipo de configuración admite varias configuraciones.  
  
 **Agregar**  
 Agrega una configuración empleando el Asistente para la configuración de paquetes.  
  
 **Editar**  
 Edita una configuración existente volviendo a ejecutar el Asistente para la configuración de paquetes.  
  
 **Quitar**  
 Seleccione una configuración y haga clic en **Quitar**.  
  
 **Flechas**  
 Seleccione una configuración y utilice las flechas arriba y abajo para subirla o bajarla de la lista. Las configuraciones se cargan en la secuencia en la que aparecen en la lista.  
  
## <a name="see-also"></a>Vea también  
 [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)  
  
  
