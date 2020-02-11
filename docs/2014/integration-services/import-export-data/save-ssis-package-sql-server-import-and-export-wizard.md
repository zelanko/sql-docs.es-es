---
title: Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 6af26cafd4f8dd9bf874ae7860c4f796bef48ae1
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62892773"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server)
  Use la **Página guardar el paquete SSIS** para asignar un nombre, describir y [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] guardar un[!INCLUDE[ssIS](../../includes/ssis-md.md)]paquete de Integration Services ( [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` ) en la base de datos o en un archivo que tenga la extensión. DTSX.  
  
> [!NOTE]  
>  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la opción para guardar el paquete creado por el asistente no está disponible.  
  
 Para obtener más información acerca de este asistente, vea [Asistente para importación y exportación de SQL Server](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, vea [ejecutar el Asistente para importación y exportación de SQL Server](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Nombre**  
 Escriba un nombre único para el paquete.  
  
 **Descripción**  
 Escriba una descripción para el paquete. Como práctica recomendada, describa el paquete en función de su objetivo para que los paquetes se documenten por sí mismos y su mantenimiento resulte sencillo.  
  
 **Dirigir**  
 Vea el destino (de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o un archivo) especificado previamente como archivo de destino.  
  
## <a name="target-dynamic-options"></a>Opciones dinámicas de destino  
  
### <a name="target--sql-server"></a>Destino = SQL Server  
 **Nombre del servidor**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba o seleccione el nombre del servidor de destino.  
  
 **Usar autenticación de Windows**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique si desea conectarse al servidor a través de la autenticación de Windows integrada. Éste es el método de autenticación preferido.  
  
 **Usar autenticación SQL Server**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique si desea conectarse al servidor a través de la autenticación de SQL Server.  
  
 **Nombre de usuario**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que haya especificado la autenticación de SQL Server, escriba el nombre de usuario de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 **Contraseña**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que haya especificado la autenticación de SQL Server, escriba la contraseña de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="target--file-system"></a>Destino = Sistema de archivos  
 **Nombre de archivo**  
 Cuando haya seleccionado un destino de archivo, escriba la ruta de acceso del archivo de destino o use el botón **examinar** .  
  
 **Browse**  
 Cuando haya seleccionado un destino de archivo, vaya al archivo de destino mediante el cuadro de diálogo **Guardar paquete** .  
  
## <a name="see-also"></a>Consulte también  
 [Guardar paquetes](../save-packages.md)  
  
  
