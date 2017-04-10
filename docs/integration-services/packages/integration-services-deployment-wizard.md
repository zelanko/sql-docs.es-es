---
title: "Asistente para implementaci&#243;n de Integration Services | Microsoft Docs"
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
  - "sql13.ssis.deploymentwizard.f1"
ms.assetid: f3d93e13-2d85-47ff-a913-cda4046491c4
caps.latest.revision: 14
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 14
---
# Asistente para implementaci&#243;n de Integration Services
  El **Asistente para implementación de Integration Services ** admite dos modelos de implementación:
   - Modelo de implementación de proyectos
   - Modelo de implementación de paquetes 
   
 El **modelo de implementación de proyectos** permite implementar un proyecto de SQL Server Integration Services (SSIS) como una sola unidad en el catálogo de SSIS.
 
 El **modelo de implementación de paquetes** permite implementar paquetes que se han actualizado en el catálogo de SSIS sin tener que implementar todo el proyecto. 
 
 > **NOTA:** La implementación predeterminada del asistente es el modelo de implementación de proyectos.  
  
## Inicio del asistente
Inicie el asistente de una de estas dos formas:

 - Escriba **"Asistente de implementación de SQL Server"** en Windows Search 

**O BIEN**

 - Busque el archivo ejecutable **ISDeploymentWizard.exe** en la carpeta de instalación de SQL Server; por ejemplo: "C:\Archivos de programa (x86)\Microsoft SQL Server\130\DTS\Binn". 
 
 > **NOTA:** Si ve la página **Introducción**, haga clic en **Siguiente** para cambiar a la página **Seleccionar origen**. 
 
 La configuración de esta página es diferente en cada modelo de implementación. Siga los pasos de la sección [Project Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#ProjectModel) o [Package Deployment Model](../../integration-services/packages/integration-services-deployment-wizard.md#PackageModel) en función del modelo que haya seleccionado en esta página.  
  
##  <a name="ProjectModel"></a> Modelo de implementación de proyectos  
  
### Seleccionar origen  
 Para implementar un archivo de implementación de proyectos que haya creado, seleccione **Archivo de implementación de proyecto** y especifique la ruta de acceso del archivo .ispac. Para implementar un proyecto que resida en el catálogo de [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , seleccione **Catálogo de Integration Services**y especifique el nombre del servidor y la ruta de acceso al proyecto en el catálogo. Haga clic en **Siguiente** para ver la página **Seleccionar destino** .  
  
### Seleccionar destino  
 Para seleccionar la carpeta de destino para el proyecto en el catálogo [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , escriba la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o haga clic en **Examinar** para seleccionarla en una lista de servidores. Escriba la ruta de acceso del proyecto en SSISDB o haga clic en **Examinar** para seleccionarla. Haga clic en **Siguiente** para ver la página **Revisión** .  
  
### Revisión e implementación  
 La página permite revisar la configuración seleccionada. Puede cambiar las selecciones si hace clic en **Anterior**o si hace clic en cualquiera de los pasos del panel izquierdo. Haga clic en **Implementar** para iniciar el proceso de implementación.  
  
### Resultado  
 Una vez completado el proceso de implementación, debería ver la página **Resultados** . Esta página muestra si cada acción si se completó correctamente o no. Si la acción no se realiza correctamente, haga clic en **Error** en la columna **Resultado** para que aparezca una explicación del error. Haga clic en **Guardar informe** para guardar los resultados en un archivo XML o haga clic en **Cerrar** para salir del asistente.  
  
##  <a name="PackageModel"></a> Modelo de implementación de paquetes  
  
### Seleccionar origen  
 La página **Seleccionar origen** del **Asistente para implementación de Integration Services** muestra la configuración específica del modelo de implementación de paquetes cuando selecciona la opción **lmplementación del paquete** del **modelo de implementación**.  
  
 Para seleccionar los paquetes de origen, haga clic en el botón **Examinar** para seleccionar la **carpeta** that contains the packages or type the carpeta path in the **Packages carpeta path** (Ruta de acceso de la carpeta de paquetes) y haga clic en la opción **Actualizar** situada en la parte inferior de la página. Ahora, debería ver todos los paquetes en la carpeta especificada en el cuadro de lista. De forma predeterminada, se seleccionan todos los paquetes. Haga clic en la **casilla** de la primera columna para elegir los paquetes que desea implementar en el servidor.  
  
 Consulte las columnas **Estado** y **Mensaje** para comprobar el estado del paquete. Si el estado es **Listo** o **Advertencia**, el Asistente para la implementación no bloquearía el proceso de implementación. Mientras que, si el estado es **Error**, el asistente no implementará los paquetes seleccionados. Para ver los mensajes de advertencia o error detallados, haga clic en el vínculo de la columna **Mensaje**.  
  
 Si la información confidencial o los datos del paquete están cifrados con una contraseña, escríbala en la columna **Contraseña** y haga clic en el botón **Actualizar** para comprobar si se acepta la contraseña. Si la contraseña es correcta, el estado cambiaría a **Listo** y desaparecerá el mensaje de advertencia. Si hay varios paquetes con la misma contraseña, seleccione los paquetes con la misma contraseña de cifrado, escriba la contraseña en el cuadro de texto **Contraseña** y haga clic en el botón **Aplicar** . La contraseña se aplicaría a los paquetes seleccionados.  
  
 Si el estado de todos los paquetes seleccionados no es **Error**, el botón **Siguiente** se habilitará para que pueda continuar con el proceso de implementación de paquetes.  
  
### Seleccionar destino  
 Después de seleccionar los orígenes de paquetes, haga clic en el botón **Siguiente** para cambiar a la página **Seleccionar destino** . Los paquetes deben implementarse en un proyecto del catálogo de SSIS (SSISDB). Por lo tanto, antes de implementar paquetes, asegúrese de que el proyecto de destino ya exista en el catálogo de SSIS. De lo contrario, cree un proyecto vacío. En la página **Seleccionar destino** , escriba el nombre del servidor en el cuadro de texto **Nombre del servidor** o haga clic en el botón **Examinar** para seleccionar una instancia de servidor. Después, haga clic en el botón **Examinar** situado junto al cuadro de texto **Ruta** para especificar el proyecto de destino. Si el proyecto no existe, haga clic en **Nuevo proyecto** para crear un proyecto vacío como proyecto de destino. El proyecto **DEBE** crearse en una carpeta.  
  
### Revisión e implementación  
 Haga clic en la opción **Siguiente** de la página **Seleccionar destino** para cambiar a la página **Revisión** del **Asistente para implementación de Integration Services**. En esta página, revise el informe de resumen sobre la acción de implementación. Después de la comprobación, haga clic en el botón **Implementar** para realizar la acción de implementación.  
  
### Resultado  
 Una vez completada la implementación, debería ver la página **Resultados** . En la página **Resultados** , revise los resultados de cada paso del proceso de implementación. En la página **Resultados** , haga clic en **Guardar informe** para guardar el informe de implementación o **Cerrar** para cerrar el asistente.  
  
## Vea también  
 [Implementar proyectos en el servidor de Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)   
 [Implementación de proyectos y paquetes](https://msdn.microsoft.com/library/hh213290.aspx)  
  
  