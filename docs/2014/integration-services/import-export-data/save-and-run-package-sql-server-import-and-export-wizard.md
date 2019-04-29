---
title: Guarde y ejecute el paquete (importación de SQL Server y el Asistente para exportación) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.saveschedule.f1
ms.assetid: b582c462-3d7a-4a4c-a2a2-2c79fedab75a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 517ba30e4565ec05e5fa15a650bb39909d24dd02
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62894769"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Guardar y ejecutar el paquete (Asistente para importación y exportación de SQL Server)
  Use la **guardar y ejecutar paquete** cuadro de diálogo para ejecutar el paquete inmediatamente, guardado para ejecutarlo más tarde, o ambos.  
  
> [!NOTE]  
>  Si detiene un paquete antes de que termine la ejecución, no se guarda el paquete, incluso si ha seleccionado la **guardar** casilla de verificación.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información acerca de las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Ejecutar inmediatamente**  
 Seleccione esta opción para ejecutar inmediatamente el paquete.  
  
 **Guardar el paquete SSIS**  
 Guarde el paquete para ejecutarlo más tarde, con la opción de ejecutarlo inmediatamente.  
  
> [!NOTE]  
>  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la opción para guardar el paquete creado por el asistente no está disponible.  
  
 **SQL Server**  
 Seleccione esta opción para guardar el paquete en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` base de datos.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la **guardar el paquete SSIS** opción.  
  
 **Sistema de archivos**  
 Seleccione esta opción para guardar el paquete como un archivo con la extensión .dtsx.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la **guardar el paquete SSIS** opción.  
  
 **Nivel de protección de paquetes**  
 Seleccione un nivel de protección de la lista.  
  
 El nivel de protección determina el método de protección, la contraseña o la clave de usuario, así como el ámbito de protección de paquetes. La protección puede incluir todos los datos o solo los datos confidenciales. Para comprender los requisitos y opciones de seguridad de paquetes, consulte [Control del acceso a datos confidenciales en paquetes](../security/access-control-for-sensitive-data-in-packages.md) y [información general sobre seguridad &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la **guardar el paquete SSIS** opción.  
  
 **Contraseña**  
 Escriba una contraseña.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha establecido la **nivel de protección de paquetes** opción **cifrar información confidencial con contraseña** o **cifrar todos los datos con una contraseña**.  
  
 **Volver a escribir la contraseña**  
 Escriba la contraseña nuevamente.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha establecido la **nivel de protección de paquetes** opción **cifrar información confidencial con contraseña** o **cifrar todos los datos con una contraseña**.  
  
## <a name="see-also"></a>Vea también  
 [Execution of Projects and Packages](../packages/run-integration-services-ssis-packages.md)  (Ejecución de proyectos y paquetes)  
 [Guardar paquetes](../save-packages.md)  
  
  
