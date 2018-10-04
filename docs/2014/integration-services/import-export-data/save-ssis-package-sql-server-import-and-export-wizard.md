---
title: Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.impexpwizard.savedtspackage.f1
ms.assetid: 7bf8ac6a-5599-43ab-bf5c-e072c11b85a0
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 8b8ef62839d7379c35b55af7bcb65ab46e4b455d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48048237"
---
# <a name="save-ssis-package-sql-server-import-and-export-wizard"></a>Guardar el paquete SSIS (Asistente para importación y exportación de SQL Server)
  Use la **guardar el paquete SSIS** página Nombre, describir y guardar un [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Integration Services ([!INCLUDE[ssIS](../../includes/ssis-md.md)]) del paquete para el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `msdb` de base de datos o a un archivo que tiene el dtsx extensión.  
  
> [!NOTE]  
>  En [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], la opción para guardar el paquete creado por el asistente no está disponible.  
  
 Para más información acerca de este asistente, consulte [SQL Server Import and Export Wizard](import-and-export-data-with-the-sql-server-import-and-export-wizard.md). Para obtener información sobre las opciones para iniciar el asistente y sobre los permisos necesarios para ejecutar el asistente correctamente, consulte [ejecutar la importación de SQL Server y el Asistente para exportación de](start-the-sql-server-import-and-export-wizard.md).  
  
 La finalidad del Asistente para importación y exportación de SQL Server es copiar datos desde un origen a un destino. El asistente también puede crear una base de datos y tablas de destino. Sin embargo, si tiene que copiar diversas bases de datos o tablas, u otros tipos de objetos de bases de datos, debe utilizar el Asistente para copiar bases de datos. Para más información, consulte [Use the Copy Database Wizard](../../relational-databases/databases/use-the-copy-database-wizard.md).  
  
## <a name="static-options"></a>Opciones estáticas  
 **Nombre**  
 Escriba un nombre único para el paquete.  
  
 **Descripción**  
 Escriba una descripción para el paquete. Como práctica recomendada, describa el paquete en función de su objetivo para que los paquetes se documenten por sí mismos y su mantenimiento resulte sencillo.  
  
 **Destino**  
 Ver el destino ([!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o archivo) que se especificó anteriormente para el archivo de destino.  
  
## <a name="target-dynamic-options"></a>Opciones dinámicas de destino  
  
### <a name="target--sql-server"></a>Destino = SQL Server  
 **Nombre del servidor**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba o seleccione el nombre del servidor de destino.  
  
 **Utilizar autenticación de Windows**  
 Una vez que haya seleccionado un destino de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], especifique si desea conectarse al servidor a través de la autenticación de Windows integrada. Éste es el método de autenticación preferido.  
  
 **Utilizar autenticación de SQL Server**  
 Cuando haya seleccionado un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, especifique si desea conectarse al servidor mediante el uso de autenticación de SQL Server.  
  
 **Nombre de usuario.**  
 Cuando haya seleccionado un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, y que haya especificado la autenticación de SQL Server, escriba el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nombre de usuario.  
  
 **Contraseña**  
 Cuando haya seleccionado un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] destino, y que haya especificado la autenticación de SQL Server, escriba el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contraseña.  
  
### <a name="target--file-system"></a>Destino = Sistema de archivos  
 **Nombre de archivo**  
 Cuando haya seleccionado un destino de archivo, escriba la ruta de acceso del archivo de destino, o utilice el **examinar** botón.  
  
 **Examinar**  
 Cuando haya seleccionado un destino de archivo, busque el archivo de destino mediante el **guardar el paquete** cuadro de diálogo.  
  
## <a name="see-also"></a>Vea también  
 [Guardar paquetes](../save-packages.md)  
  
  
