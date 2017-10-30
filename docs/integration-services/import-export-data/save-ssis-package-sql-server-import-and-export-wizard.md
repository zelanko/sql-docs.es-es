---
title: Guardar el paquete SSIS (SQL Server importar y exportar) | Documentos de Microsoft
ms.custom: 
ms.date: 02/17/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: c3e47e4a5ae297202ba43679fba393421880a7ea
ms.openlocfilehash: 6ebbab742350e6874b86213c1fbf516e095a1e9a
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server)
  Si ha especificado en el **guardar y ejecutar paquete** página que desea guardar la configuración como un paquete de SQL Server Integration Services (SSIS), el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra Import and Export Wizard **guardar el paquete SSIS**. En esta página, especifique opciones adicionales para guardar el paquete creado por el asistente.  

Las opciones que se ven en la página **Guardar el paquete SSIS** dependen de la elección realizada anteriormente en la página **Guardar y ejecutar paquete** para guardar el paquete en SQL Server o en el sistema de archivos. Para echar otro vistazo a la página **Guardar y ejecutar paquete** , vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**¿Qué es un paquete?** El asistente usa SQL Server Integration Services (SSIS) para copiar datos. En SSIS, la unidad básica es el paquete. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.

## <a name="screen-shot---common-options"></a>Captura de pantalla de - opciones comunes
La captura de pantalla siguiente muestra la primera parte de la **guardar el paquete SSIS** página del asistente. El resto de la página tiene un número variable de opciones que depende el destino del paquete que eligió.

![Guardar paquete - opciones comunes](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>Proporcionar un nombre y una descripción para el paquete  
 **Nombre**  
 Escriba un nombre único para el paquete.  
  
 **Descripción**  
 Escriba una descripción para el paquete. Como procedimiento recomendado, describa el fin del paquete para que los paquetes se documenten por sí mismos y su mantenimiento resulte más sencillo.  
  
 **Destino**  
 El destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sistema de archivos) que ha especificado previamente para el paquete. Si quiere guardar el paquete en otro destino, vuelva a la página **Guardar y ejecutar paquete** .

## <a name="screen-shot---save-the-package-in-sql-server"></a>Captura de pantalla: guardar el paquete en SQL Server

 La siguiente captura de pantalla muestra la **guardar el paquete SSIS** página del asistente si seleccionó la **SQL Server** opción el **guardar y ejecutar paquete** página. 
  
![Guarde la página paquete de SSIS de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/save-package2.png "página Guardar el paquete SSIS de la importación y el Asistente para exportación")  

## <a name="options-to-specify-target--sql-server"></a>Opciones para especificar (destino = SQL Server) 

 > [!NOTE]
 > El asistente guarda el paquete en el **msdb** en la base de datos la **sysssispackages** tabla. Esta opción produce **no** guardar el paquete en la base de datos de catálogo de SSIS (SSISDB).  
 
 **Nombre del servidor**  
 Especifique o seleccione el nombre del servidor de destino.  
   
 **Utilizar autenticación de Windows**  
Conéctese al servidor mediante la autenticación integrada de Windows. Éste es el método de autenticación preferido.  
  
 **Utilizar autenticación de SQL Server**  
Conéctese al servidor mediante la autenticación de SQL Server.  
  
 **Nombre de usuario.**  
Si especifica autenticación de SQL Server, escriba el nombre de usuario.  
  
 **Contraseña**  
Si especifica autenticación de SQL Server, escriba la contraseña.  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Captura de pantalla: guardar el paquete en el sistema de archivos
 
La siguiente captura de pantalla muestra la **guardar el paquete SSIS** página del asistente si seleccionó la **sistema de archivos** opción el **guardar y ejecutar paquete** página. 
  
![Guarde la página paquete de SSIS de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/save-package1.png "página Guardar el paquete SSIS de la importación y el Asistente para exportación")  

## <a name="options-to-specify-target--file-system"></a>Opciones para especificar (destino = sistema de archivos)

 **Nombre de archivo**  
 Escriba la ruta de acceso y el nombre del archivo de destino o use la **examinar** botón para seleccionar un destino.  
  
> [!TIP]
> No olvide especificar una carpeta de destino, escribiéndola o examinando. Si sólo escribe el nombre de archivo sin una ruta de acceso, no sabe que el asistente guarda el paquete. Además, el Asistente puede intentar guardar el paquete en una ubicación donde no tiene permiso para guardar un archivo, con lo que se genera un error.  
>   
>  Recuerde dónde guarda el archivo de paquete.  
  
 **Examinar**  
 También puede examinar para seleccionar la ruta de acceso del archivo de destino en la **Guardar paquete** cuadro de diálogo.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Acerca de las dos páginas de opciones para guardar el paquete  
 La página **Guardar el paquete SSIS** es una de las dos páginas en las que se seleccionan opciones para guardar el paquete SSIS.  
  
-   En la página anterior, **Guardar y ejecutar paquete**, elija si quiere guardar el paquete en SQL Server o como un archivo. También puede seleccionar la configuración de seguridad para el paquete guardado. Para echar otro vistazo a la página **Guardar y ejecutar paquete** , vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
  
-   En la página actual, proporcione un nombre para el paquete y más información sobre dónde guardarlo.  
 
## <a name="run-the-saved-package-again-later"></a>Volver a ejecutar el paquete guardado más adelante  
 Para más información sobre cómo ejecutar el paquete guardado más adelante, vea uno de los siguientes temas.  
  
-   Para ejecutar un paquete mediante un programa de utilidad con una interfaz de usuario sencilla, vea [Referencia de la interfaz de usuario de la Utilidad de ejecución de paquetes &#40;DtExecUI&#41;](../../integration-services/packages/execute-package-utility-dtexecui-ui-reference.md).  
  
-   Para ejecutar un paquete desde la línea de comandos o desde un archivo por lotes, vea [Utilidad dtexec](../../integration-services/packages/dtexec-utility.md).  
  
-   Si guardó el paquete en SQL Server en la base de datos **msdb** , conéctese con el servicio de Integration Services. Luego, en SQL Server Management Studio, en el Explorador de objetos, vaya a **Paquetes almacenados | MSDB**, haga clic con el botón derecho en el paquete y seleccione **Ejecutar paquete**.

-   Si guardó el paquete en el sistema de archivos, vea [Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md) para ejecutar el paquete en el entorno de desarrollo. Para poder abrirlo y ejecutarlo, tiene que agregar el paquete a un proyecto de Integration Services.  

## <a name="customize-the-saved-package"></a>Personalizar el paquete guardado  
 Para más información sobre cómo personalizar el paquete guardado, vea [Paquetes de Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-packages.md).  
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de especificar opciones adicionales para guardar el paquete, la página siguiente es **Complete el asistente**. En esta página, revise las opciones seleccionadas en el asistente y luego inicie la operación. Para obtener más información, vea [Finalización del asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>Vea también  
[Guardar paquetes](../../integration-services/save-packages.md)  
[Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 

