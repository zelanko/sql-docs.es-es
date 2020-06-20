---
title: Guardar y ejecutar el paquete (Asistente para importación y exportación de SQL Server) | Microsoft Docs
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
ms.openlocfilehash: c3b1be3f11e3a53ad291ff774cc72468af0d66ca
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84966232"
---
# <a name="save-and-execute-package-sql-server-import-and-export-wizard"></a>Guardar y ejecutar el paquete (Asistente para importación y exportación de SQL Server)
  Utilice el cuadro de diálogo **Guardar y ejecutar paquete** para ejecutar el paquete inmediatamente, guardarlo para ejecutarlo más tarde o ambos.  
  
> [!NOTE]  
>   Si detiene el paquete antes de que termine la ejecución, éste no se guardará, aunque haya activado la casilla **Guardar** .  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente, así como los permisos necesarios para ejecutar el asistente correctamente, vea [ejecutar el Asistente para importación y exportación de SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="options"></a>Opciones  
 **Ejecutar inmediatamente**  
 Seleccione esta opción para ejecutar inmediatamente el paquete.  
  
 **Guardar el paquete SSIS**  
 Guarde el paquete para ejecutarlo más tarde, con la opción de ejecutarlo inmediatamente.  
  
> [!NOTE]  
>  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] , la opción para guardar el paquete creado por el asistente no está disponible.  
  
 **SQL Server**  
 Seleccione esta opción para guardar el paquete en la [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` base de datos.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **guardar el paquete SSIS** .  
  
 **Sistema de archivos**  
 Seleccione esta opción para guardar el paquete como un archivo con la extensión .dtsx.  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **guardar el paquete SSIS** .  
  
 **Nivel de protección de paquetes**  
 Seleccione un nivel de protección de la lista.  
  
 El nivel de protección determina el método de protección, la contraseña o la clave de usuario, así como el ámbito de protección de paquetes. La protección puede incluir todos los datos o solo los datos confidenciales. Para comprender los requisitos y las opciones de seguridad de los paquetes, consulte [Access Control de datos confidenciales en paquetes](../security/access-control-for-sensitive-data-in-packages.md) e [información general sobre seguridad &#40;Integration Services&#41;](../security/security-overview-integration-services.md).  
  
> [!NOTE]  
>  Esta opción solo está disponible si ha seleccionado la opción **guardar el paquete SSIS** .  
  
 **Contraseña**  
 Escriba una contraseña.  
  
> [!NOTE]  
>  Esta opción solo está disponible si se ha establecido la opción **nivel de protección de paquetes** en **cifrar la información confidencial con una contraseña** o **cifrar todos los datos con una contraseña**.  
  
 **Volver a escribir la contraseña**  
 Escriba la contraseña nuevamente.  
  
> [!NOTE]  
>  Esta opción solo está disponible si se ha establecido la opción **nivel de protección de paquetes** en **cifrar la información confidencial con una contraseña** o **cifrar todos los datos con una contraseña**.  
  
## <a name="see-also"></a>Consulte también  
 [Ejecución de proyectos y paquetes](../packages/run-integration-services-ssis-packages.md)   
 [Guardar paquetes](../save-packages.md)  
  
  
