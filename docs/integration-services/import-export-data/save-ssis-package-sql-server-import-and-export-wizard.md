---
title: Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/17/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
caps.latest.revision: 64
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 9f29b9614d13e0d438e5fc0f2d850f3d6b77f6e1
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/12/2018
ms.locfileid: "35401247"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server)
  Si en la página **Guardar y ejecutar el paquete** especificó que quiere guardar la configuración como un paquete de SQL Server Integration Services (SSIS), el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Guardar el paquete SSIS**. En esta página, especifique opciones adicionales para guardar el paquete que creó el asistente.  

Las opciones que se ven en la página **Guardar el paquete SSIS** dependen de la elección realizada anteriormente en la página **Guardar y ejecutar paquete** para guardar el paquete en SQL Server o en el sistema de archivos. Para echar otro vistazo a la página **Guardar y ejecutar paquete** , vea [Guardar y ejecutar paquete](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).
 
**¿Qué es un paquete?** El asistente usa SQL Server Integration Services (SSIS) para copiar datos. En SSIS, la unidad básica es el paquete. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.

## <a name="screen-shot---common-options"></a>Captura de pantalla (opciones comunes)
En la captura de pantalla siguiente se muestra la primera parte de la página **Guardar el paquete SSIS** del asistente. El resto de la página tiene un número variable de opciones que dependen del destino del paquete que elija.

![Guardar paquete (opciones comunes)](../../integration-services/import-export-data/media/save-package-common-options.png)

## <a name="provide-a-name-and-description-for-the-package"></a>Proporcionar un nombre y una descripción para el paquete  
 **Nombre**  
 Escriba un nombre único para el paquete.  
  
 **Descripción**  
 Escriba una descripción para el paquete. Como procedimiento recomendado, describa el fin del paquete para que los paquetes se documenten por sí mismos y su mantenimiento resulte más sencillo.  
  
 **Destino**  
 El destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o sistema de archivos) que ha especificado previamente para el paquete. Si quiere guardar el paquete en otro destino, vuelva a la página **Guardar y ejecutar paquete** .

## <a name="screen-shot---save-the-package-in-sql-server"></a>Captura de pantalla: guardar el paquete en SQL Server

 La siguiente captura de pantalla muestra la página **Guardar el paquete SSIS** del asistente si seleccionó la opción **SQL Server** en la página **Guardar y ejecutar el paquete**. 
  
![Página Guardar el paquete SSIS del Asistente para importación y exportación](../../integration-services/import-export-data/media/save-package2.png "Página Guardar el paquete SSIS del Asistente para importación y exportación")  

## <a name="options-to-specify-target--sql-server"></a>Opciones que hay que especificar (Destino = SQL Server) 

 > [!NOTE]
 > El asistente guarda el paquete en la base de datos **msdb** de la tabla **sysssispackages**. Esta opción **no** guarda el paquete en la base de datos del catálogo de SSIS (SSISDB).  
 
 **Nombre del servidor**  
 Especifique o seleccione el nombre del servidor de destino.  
   
 **Utilizar autenticación de Windows**  
Conéctese al servidor mediante la autenticación integrada de Windows. Éste es el método de autenticación preferido.  
  
 **Utilizar autenticación de SQL Server**  
Conéctese al servidor mediante la autenticación de SQL Server.  
  
 **User name**  
Si ha especificado la autenticación de SQL Server, escriba el nombre de usuario.  
  
 **Contraseña**  
Si ha especificado la autenticación de SQL Server, escriba la contraseña.  
    
## <a name="screen-shot---save-the-package-in-the-file-system"></a>Captura de pantalla: guardar el paquete en el sistema de archivos
 
La siguiente captura de pantalla muestra la página **Guardar el paquete SSIS** del asistente si seleccionó la opción **Sistema de archivos** en la página **Guardar y ejecutar el paquete**. 
  
![Página Guardar el paquete SSIS del Asistente para importación y exportación](../../integration-services/import-export-data/media/save-package1.png "Página Guardar el paquete SSIS del Asistente para importación y exportación")  

## <a name="options-to-specify-target--file-system"></a>Opciones que hay que especificar (Destino = Sistema de archivos)

 **Nombre de archivo**  
 Para seleccionar un destino, escriba la ruta de acceso y el nombre del archivo de destino o use el botón **Examinar**.  
  
> [!TIP]
> Asegúrese de especificar una carpeta de destino mediante su escritura o exploración. Si solo escribe el nombre de archivo sin una ruta de acceso, no sabrá dónde guarda el paquete el asistente. Además, el Asistente puede intentar guardar el paquete en una ubicación donde no tiene permiso para guardar un archivo, con lo que se genera un error.  
>   
>  Recuerde dónde guarda el archivo de paquete.  
  
 **Examinar**  
 Opcionalmente, examine para seleccionar la ruta de acceso del archivo de destino en el cuadro de diálogo **Guardar paquete**.  

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
  
## <a name="whats-next"></a>¿Qué sigue?  
 Después de especificar opciones adicionales para guardar el paquete, la página siguiente es **Complete el asistente**. En esta página, revise las opciones seleccionadas en el asistente y luego inicie la operación. Para obtener más información, vea [Finalización del asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
 
## <a name="see-also"></a>Ver también  
[Guardar paquetes](../../integration-services/save-packages.md)  
[Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)
 
 
