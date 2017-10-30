---
title: "Guardar y ejecutar paquete (importación de SQL Server y Asistente para exportación) | Documentos de Microsoft"
ms.custom: 
ms.date: 02/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
caps.latest.revision: 69
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f5acdf3ae4f27685fce7aab56aab423044491ee1
ms.openlocfilehash: 40b8677cddf363e8789a2fc15b1c2aab5f49f58c
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Guardar y ejecutar paquete (importación de SQL Server y Asistente para exportación)
  Después de especificar y configurar el origen y el destino de los datos, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Guardar y ejecutar el paquete**. En esta página, especifique si quiere ejecutar la operación de copia inmediatamente. Según la configuración, también puede guardar la configuración como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] paquete (SSIS) para personalizarla y volver a usarla más adelante.
  
**¿Qué es un paquete?** El asistente usa SQL Server Integration Services (SSIS) para copiar datos. En SSIS, la unidad básica es el paquete. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Captura de pantalla de la página Guardar y ejecutar el paquete  
En la captura de pantalla siguiente se muestra la página **Guardar y ejecutar el paquete** del asistente. 
   
![Guarde y ejecute la página paquete de la importación y el Asistente para exportación de](../../integration-services/import-export-data/media/save-and-run.png "guardar y ejecutar la página paquete de la importación y el Asistente para exportación") 
  
## <a name="run-and-save-the-package"></a>Ejecutar y guardar el paquete 
 Para continuar, deberá seleccionar al menos una de las dos opciones siguientes.  
  
 **Run immediately**  
 Seleccione esta opción para importar y exportar datos inmediatamente. De forma predeterminada, esta casilla está activada y la operación se ejecuta inmediatamente.
  
 **Guardar el paquete SSIS**  
 Guardar la configuración como un paquete SSIS. Más adelante, si le interesa, puede personalizar el paquete y volver a ejecutarlo. Si decide guardar el paquete, hay opciones adicionales en la página siguiente, **Guardar el paquete SSIS**.
 
La opción para guardar el paquete está disponible únicamente si tiene instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o una edición superior.   
  
> [!NOTE]
> Si finaliza el asistente, ejecute la operación, pero detener la operación antes de que termine la ejecución, no se guarda el paquete, aunque haya activado el **guardar el paquete SSIS** casilla de verificación.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Si se inició al asistente desde Visual Studio
Si inicia al asistente desde un proyecto de Integration Services en Visual Studio con SQL Server Data Tools (SSDT):
-   No se puede **ejecutar** el paquete hasta después de salir del asistente. A continuación, puede ejecutar el paquete de Visual Studio.
-   El Asistente para **guarda** el paquete en el proyecto de Integration Services desde el que se inició el asistente.

## <a name="specify-options-for-saving-the-package"></a>Opciones específicas para guardar el paquete
**SQL Server**  
 Seleccione esta opción para guardar el paquete en SQL Server en el **msdb** en la base de datos la **sysssispackages** tabla.
 
> [!IMPORTANT]
> Esta opción no guarda el paquete en la base de datos del catálogo de SSIS (SSISDB).  

 Seleccione el servidor de destino y proporcione las credenciales para conectarse al servidor en la página siguiente, **Guardar el paquete SSIS**. Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Sistema de archivos**  
 Seleccione esta opción para guardar el paquete como un archivo con el **dtsx** extensión.  
  
 Seleccione la carpeta de destino y el nombre de archivo para el paquete en la página siguiente, **Guardar el paquete SSIS**. Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
 
 ## <a name="specify-the-package-protection-level"></a>Especificar el nivel de protección del paquete
 **Nivel de protección de paquetes**  
 Seleccione un nivel de protección de la lista para ayudar a proteger los datos del paquete.  
  
 El nivel de protección determina el método de protección, la contraseña o la clave de usuario, así como el ámbito de protección de paquetes. La protección puede incluir todos los datos o solo los datos confidenciales. Para obtener más información sobre las opciones disponibles, vea [Control del acceso a la información confidencial en paquetes](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
 **Contraseña**  
 Escriba una contraseña.  
  
 **Volver a escribir la contraseña**  
 Escriba la contraseña nuevamente.  
  
> [!NOTE]
> Están disponibles las opciones de contraseña solo si especifica un **nivel de protección del paquete** que requiere una contraseña: es decir, si se especifica cualquiera **cifrar información confidencial con contraseña** o **cifrar todos los datos con una contraseña**.  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Acerca de las dos páginas de opciones para guardar el paquete  
 La página **Guardar y ejecutar el paquete SSIS** es una de las dos páginas en las que se seleccionan opciones para guardar el paquete SSIS.  
  
-   En la página actual, elija si quiere guardar el paquete en SQL Server o como un archivo. También puede seleccionar la configuración de seguridad para el paquete guardado.  
  
-   Después, en la página **Guardar el paquete SSIS** , proporcione un nombre para el paquete y más información sobre dónde guardarlo. Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Estas opciones solo están disponibles si selecciona la opción **Guardar el paquete SSIS** en esta página.  
  
## <a name="whats-next"></a>¿Qué debe hacer a continuación?  
 Después de especificar si quiere ejecutar la operación de copia inmediatamente y si quiere guardar el paquete, la siguiente página depende de las opciones que elija.  
  
-   Si ha seleccionado la opción para ejecutar el paquete inmediatamente, pero no para guardarlo, la página siguiente es **Finalización del asistente**. En esta página, revise las opciones seleccionadas en el asistente y luego inicie la operación de copia. Para obtener más información, vea [Finalización del asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Si ha seleccionado la opción para guardar el paquete, la página siguiente es **Guardar el paquete SSIS**. En esta página, especifique opciones adicionales para guardar el paquete. (Una vez guardado el paquete, la página siguiente es **Finalización del asistente**). Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Vea también  
[Guardar paquetes](../../integration-services/save-packages.md)  
[Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Empezar a trabajar con este ejemplo sencillo de la importación y el Asistente para exportación](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  


