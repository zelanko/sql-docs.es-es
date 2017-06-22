---
title: "SQL Server Management Studio: notas de la versión | Microsoft Docs"
ms.custom: 
ms.date: 01/30/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0b95337b-80bf-4624-8f5d-cdaf6181d3b8
caps.latest.revision: 51
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: b68d454230d414ff52d90b4f3f71dd68ee65c6bc
ms.openlocfilehash: 1733a789fb2dc17eea82ab22d4a50614d1fffc3b
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio: notas de la versión
Bienvenido/a a nuestra versión de disponibilidad general de SQL Server Management Studio.  Esta versión de SQL Server Management Studio (SSMS) es una instalación independiente fuera de la versión de SQL Server. Nuestro objetivo es actualizarla con frecuencia con nuevas funciones, correcciones y compatibilidad para las características más recientes de SQL Server y de Base de datos SQL de Azure.  
  
Para instalar la versión más reciente de SQL Server Management Studio, vea [Download SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
A continuación indicamos los problemas y las limitaciones de esta versión de SQL Server Management Studio:  

1. **Asistente para la base de datos de restauración genera un modelo de ruta de acceso incorrecta para la ubicación del archivo de base de datos de destino** 
    trata de un problema conocido cuando SSMS está conectado a un servidor Linux. Aunque la ruta de acceso tiene un aspecto correcto/impar, que se procese correctamente en el servidor, es decir, no hay ningún problema funcional.

2. **Problemas del explorador de archivos**
    - Cuando se trabaja con una instancia basada en Windows de SQL Server de 2017 CTP 2.0, se puede producir un error en el Explorador de archivos de interfaz de usuario de SSMS abrir si el servidor tiene una unidad de disquete vacía o un disco fijo protegidas por Bitlocker instalado. 
    - La interfaz de usuario del explorador de archivos ya no es compatible con las versiones de SQL Server 2017 antes de CTP 2.0.
    


3. **Una sola cuenta de Azure Active Directory puede iniciar sesión para una instancia de SSMS utilizando la autenticación universal de Active Directory.**  
    Esta restricción se limita a la autenticación universal de Active Directory. Puede iniciar sesión en servidores diferentes mediante la autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.
    
    Como alternativa, puede utilizar otra instancia de SSMS para iniciar sesión con otra cuenta de Azure Active Directory. 
    
4. **Los comandos del marco de aplicación de capa de datos (DacFx) y el Diseñador de esquemas en SSMS no admiten la autenticación universal de Active Directory.**  
    Los comandos que utiliza DacFx (por ejemplo, importar y exportar) y el Diseñador de esquemas en SSMS no admiten actualmente la autenticación universal de Active Directory.
    
    Como solución alternativa, puede usar las otras formas de autenticación proporcionada en SSMS - autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.

5. **SSMS solo puede conectarse a instancias de SQL Server 2016 Integrated Services (SSIS 2016).**  
    Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
    
    Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la [versión SSMS alineado con la instancia SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
5. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.**  
    Se trata de una limitación conocida que esperamos solucionar en el futuro. Mientras tanto, puede usar la [versión de SSMS de 2014](../ssms/previous-sql-server-management-studio-releases.md) para guardar los planes de mantenimiento.  
    
5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**  
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.
  
## <a name="feedback"></a>Comentarios  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
[Tutorial de SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Descargar SQL Server Management Studio &amp;#40;SSMS&amp;#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Versiones anteriores de SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

