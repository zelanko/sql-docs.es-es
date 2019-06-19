---
title: Guardar y ejecutar el paquete (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/16/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 8326920e557d6ed304414f96a7da040de0093dd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65723727"
---
# <a name="save-and-run-package-sql-server-import-and-export-wizard"></a>Guardar y ejecutar el paquete (Asistente para importación y exportación de SQL Server)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Después de especificar y configurar el origen y el destino de los datos, el Asistente para importación y exportación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] muestra **Guardar y ejecutar el paquete**. En esta página, especifique si quiere ejecutar la operación de copia inmediatamente. Según la configuración, es posible que también pueda guardar su configuración como un paquete [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] (SSIS) para personalizarlo y volver a usarlo más adelante.
  
**¿Qué es un paquete?** El asistente usa SQL Server Integration Services (SSIS) para copiar datos. En SSIS, la unidad básica es el paquete. El asistente crea un paquete SSIS en la memoria a medida que se desplaza por las páginas del asistente y especifica las opciones.
  
## <a name="screen-shot-of-the-save-and-run-package-page"></a>Captura de pantalla de la página Guardar y ejecutar el paquete  
En la captura de pantalla siguiente se muestra la página **Guardar y ejecutar el paquete** del asistente. 
   
![Página Guardar y ejecutar el paquete del Asistente para importación y exportación](../../integration-services/import-export-data/media/save-and-run.png "Página Guardar y ejecutar el paquete del Asistente para importación y exportación") 
  
## <a name="run-and-save-the-package"></a>Ejecutar y guardar el paquete 
 Para continuar, deberá seleccionar al menos una de las dos opciones siguientes.  
  
 **Run immediately**  
 Seleccione esta opción para importar y exportar datos inmediatamente. Esta casilla está activada de forma predeterminada y la operación se ejecuta de inmediato.
  
 **Guardar el paquete SSIS**  
 Guarde la configuración como un paquete SSIS. Más adelante, si le interesa, puede personalizar el paquete y volver a ejecutarlo. Si decide guardar el paquete, hay opciones adicionales en la página siguiente, **Guardar el paquete SSIS**.
 
La opción para guardar el paquete está disponible únicamente si tiene instalado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Standard Edition o una edición superior.   
  
> [!NOTE]
> Si finaliza el asistente y ejecuta la operación, pero la detiene antes de que termine de ejecutarse, el paquete no se guardará, aunque haya activado la casilla **Guardar paquete SSIS** en esta página.  

### <a name="if-you-started-the-wizard-from-visual-studio"></a>Si inició al asistente desde Visual Studio
Si inició el asistente desde un proyecto de Integration Services en Visual Studio con SQL Server Data Tools (SSDT):
-   Para **ejecutar** el paquete, debe salir del asistente. A continuación, puede ejecutar el paquete desde Visual Studio.
-   El asistente **guarda** el paquete en el proyecto de Integration Services desde el que se inició el asistente.

## <a name="specify-options-for-saving-the-package"></a>Opciones específicas para guardar el paquete
**SQL Server**  
 Seleccione esta opción para guardar el paquete en SQL Server en la base de datos **msdb** de la tabla **sysssispackages**.
 
> [!IMPORTANT]
> Esta opción no guarda el paquete en la base de datos del catálogo de SSIS (SSISDB).  

 Seleccione el servidor de destino y proporcione las credenciales para conectarse al servidor en la página siguiente, **Guardar el paquete SSIS**. Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 **Sistema de archivos**  
 Seleccione esta opción para guardar el paquete como un archivo con la extensión **.dtsx**.  
  
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
> Las opciones de contraseña solo están disponibles si ha especificado un **Nivel de protección de paquetes** que requiera una contraseña (es decir, **Cifrar la información confidencial con una contraseña** o **Cifrar todos los datos con una contraseña**).  

## <a name="about-the-two-pages-of-options-for-saving-the-package"></a>Acerca de las dos páginas de opciones para guardar el paquete  
 La página **Guardar y ejecutar el paquete SSIS** es una de las dos páginas en las que se seleccionan opciones para guardar el paquete SSIS.  
  
-   En la página actual, elija si quiere guardar el paquete en SQL Server o como un archivo. También puede seleccionar la configuración de seguridad para el paquete guardado.  
  
-   Después, en la página **Guardar el paquete SSIS** , proporcione un nombre para el paquete y más información sobre dónde guardarlo. Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
 Estas opciones solo están disponibles si selecciona la opción **Guardar el paquete SSIS** en esta página.  
  
## <a name="whats-next"></a>¿Qué sigue?  
 Después de especificar si quiere ejecutar la operación de copia inmediatamente y si quiere guardar el paquete, la siguiente página depende de las opciones que elija.  
  
-   Si ha seleccionado la opción para ejecutar el paquete inmediatamente, pero no para guardarlo, la página siguiente es **Finalización del asistente**. En esta página, revise las opciones seleccionadas en el asistente y luego inicie la operación de copia. Para obtener más información, vea [Finalización del asistente](../../integration-services/import-export-data/complete-the-wizard-sql-server-import-and-export-wizard.md).  
  
-   Si ha seleccionado la opción para guardar el paquete, la página siguiente es **Guardar el paquete SSIS**. En esta página, especifique opciones adicionales para guardar el paquete. (Una vez guardado el paquete, la página siguiente es **Finalización del asistente**). Para obtener más información, vea [Guardar el paquete SSIS](../../integration-services/import-export-data/save-ssis-package-sql-server-import-and-export-wizard.md).  
  
## <a name="see-also"></a>Consulte también  
[Guardar paquetes](../../integration-services/save-packages.md)  
[Ejecutar paquetes de Integration Services (SSIS)](../../integration-services/packages/run-integration-services-ssis-packages.md)  
[SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
[Comenzar con este sencillo ejemplo del Asistente para importar y exportar](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md)

  

