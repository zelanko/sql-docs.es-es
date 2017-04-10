---
title: "Organizador de configuraciones de paquetes | Microsoft Docs"
ms.custom: ""
ms.date: "08/25/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.packageconfigurationorganizer.f1"
helpviewer_keywords: 
  - "Organizador de configuraciones de paquetes, cuadro de diálogo"
ms.assetid: f20ae6cb-9e6a-4d24-88ff-d7a903a4e8d3
caps.latest.revision: 39
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 39
---
# Organizador de configuraciones de paquetes
  Utilice el cuadro de diálogo **Organizador de configuraciones de paquetes** para habilitar las configuraciones de paquetes, ver una lista de configuraciones para el paquete actual y especificar el orden de preferencia en el que se deben cargar las configuraciones.  
  
> **NOTA:** Hay configuraciones disponibles para el modelo de implementación de paquetes. Se usan parámetros en lugar de configuraciones para el modelo de implementación de proyectos. El modelo de implementación de proyectos le permite implementar proyectos de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] en el servidor de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . Para obtener más información acerca de los modelos de implementación, vea [Deployment of Projects and Packages](https://msdn.microsoft.com/library/hh213290.aspx).  
  
 Si varias configuraciones actualizan la misma propiedad, los valores de las configuraciones que aparezcan más abajo en la lista reemplazarán los valores de aquéllas que ocupen un lugar superior en la lista. El último valor cargado en la propiedad es el valor que se usa cuando se ejecuta el paquete. Asimismo, si el paquete utiliza una combinación de configuración directa, como un archivo de configuración XML, y configuración indirecta, como una variable de entorno, la configuración indirecta que señala a la ubicación de la configuración directa debe ocupar un lugar superior en la lista.  
  
> **NOTA:** Cuando las configuraciones de paquetes se cargan en el orden preferido, se cargan de arriba a abajo, según la lista que se muestra en el cuadro de diálogo **Organizador de configuraciones de paquetes**. Sin embargo, en tiempo de ejecución, las configuraciones de paquetes podrían no cargarse en el orden preferido. Concretamente, las configuraciones de paquetes principales se cargan después de las configuraciones de otros tipos.  
  
 Las configuraciones de paquetes actualizan los valores de las propiedades de los objetos de paquete en tiempo de ejecución. Cuando se carga un paquete, los valores de las configuraciones reemplazan los valores establecidos cuando se desarrolló el paquete. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] admite distintos tipos de configuración. Por ejemplo, se puede utilizar un archivo XML que contenga múltiples configuraciones o una variable de entorno que contenga una única configuración. Para más información, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
## Opciones  
 **Habilitar configuraciones de paquetes**  
 Seleccione esta opción para utilizar las configuraciones incluidas con el paquete.  
  
 **Nombre de la configuración**  
 Presenta el nombre de la configuración.  
  
 **Tipo de configuración**  
 Presenta el tipo de la ubicación donde se almacenan las configuraciones.  
  
 **Cadena de configuración**  
 Presenta la ubicación donde se almacenan los valores de configuración. La ubicación puede ser la ruta de acceso a un archivo, el nombre de una variable de entorno, el nombre de una variable de paquete principal, una clave del Registro o el nombre de una tabla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
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
  
## Vea también  
 [Crear configuraciones de paquetes](../../integration-services/packages/create-package-configurations.md)  
  
  