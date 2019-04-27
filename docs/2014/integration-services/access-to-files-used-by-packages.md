---
title: Acceso a los archivos usados por los paquetes | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- packages [Integration Services], security
- configuration files [Integration Services]
- checkpoint files
- Integration Services packages, security
- logs [Integration Services], security
- files [Integration Services], security
- SQL Server Integration Services packages, security
ms.assetid: 2e3ddea9-5289-4289-a70e-11c018f34977
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: eed6f09197585e7eb8575c43146ed730497af8a0
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62772261"
---
# <a name="access-to-files-used-by-packages"></a>Acceso a los archivos usados por los paquetes
  El nivel de protección de paquetes no protege los archivos almacenados fuera del paquete. Entre los archivos figuran los siguientes:  
  
-   Archivos de configuración  
  
-   punto de comprobación, archivos  
  
-   Archivos de registro  
  
 Estos archivos se deben proteger por separado, especialmente si incluyen información confidencial.  
  
## <a name="configuration-files"></a>Archivos de configuración  
 Si una configuración contiene información confidencial, como información de inicio de sesión o de la contraseña, puede guardar la configuración en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]o usar una lista de control de acceso (ACL) para restringir el acceso a la ubicación o carpeta en la que ha almacenado los archivos y para permitir el acceso solo a determinadas cuentas. Por lo general, otorgará acceso a las cuentas a las que permite ejecutar paquetes, y a las cuentas que administran paquetes y que solucionan problemas de paquetes, que pueden incluir la revisión del contenido de archivos de configuración, de punto de comprobación y de registro. [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] proporciona el almacenamiento más seguro dado que ofrece protección en los niveles de servidor y base de datos. Para guardar configuraciones en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], utilice el tipo de configuración [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para guardar configuraciones en el sistema de archivos, utilice el tipo de configuración XML.  
  
 Para más información, vea [Configuraciones de paquetes](../../2014/integration-services/package-configurations.md), [Crear configuraciones de paquetes](../../2014/integration-services/create-package-configurations.md)y [Consideraciones de seguridad para una instalación de SQL Server](../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
## <a name="checkpoint-files"></a>punto de comprobación, archivos  
 De igual modo, si el archivo de punto de comprobación que utiliza el paquete incluye información confidencial, debe utilizar una lista de control de acceso (ACL) para asegurar la ubicación o carpeta en la que ha almacenado el archivo. Los archivos de punto de comprobación guardan la información de estado actual acerca del progreso del paquete y los valores actuales de las variables. Por ejemplo, el paquete puede incluir una variable personalizada que contiene un número de teléfono. Para obtener más información, vea [Reiniciar paquetes de usando puntos de comprobación](packages/restart-packages-by-using-checkpoints.md).  
  
## <a name="log-files"></a>Archivos de registro  
 También es necesario proteger las entradas del registro escritas en el sistema de archivos mediante una lista de control de acceso (ACL). Las entradas del registro pueden almacenarse también en tablas de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] y protegerse con la seguridad de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Las entradas del registro pueden incluir información confidencial. Por ejemplo, si el paquete contiene una tarea Ejecutar SQL que crea una instrucción SQL que hace referencia a un número de teléfono, la entrada del registro de la instrucción SQL incluye el número de teléfono. La instrucción SQL puede revelar información privada acerca de los nombres de tablas y columnas de las bases de datos. Para obtener más información, vea [Registro de Integration Services &#40;SSIS&#41;](performance/integration-services-ssis-logging.md).  
  
  
