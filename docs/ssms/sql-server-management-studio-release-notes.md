---
title: "SQL Server Management Studio: notas de la versión | Microsoft Docs"
ms.custom: 
ms.date: 06/22/2017
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
ms.translationtype: HT
ms.sourcegitcommit: 223d43974e6b63f7375a3d3e000492612fb6856e
ms.openlocfilehash: 7fb0aa5f5d8b78a4783efdbb4e1f064eb025538a
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="sql-server-management-studio----release-notes"></a>SQL Server Management Studio: notas de la versión
Bienvenido/a a nuestra versión de disponibilidad general de SQL Server Management Studio.  Esta versión de SQL Server Management Studio (SSMS) es una instalación independiente fuera de la versión de SQL Server. Nuestro objetivo es actualizarla con frecuencia con nuevas funciones, correcciones y compatibilidad para las características más recientes de SQL Server y de Base de datos SQL de Azure.  
  
Para instalar la versión más reciente de SQL Server Management Studio, vea [Descargar SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md).  
  
A continuación indicamos los problemas y las limitaciones de esta versión de SQL Server Management Studio:  

1. **El asistente Restaurar base de datos genera un modelo de ruta de acceso incorrecta a la ubicación del archivo de base de datos de destino** Se trata de un problema conocido cuando SSMS está conectado a un servidor Linux. Aunque la ruta de acceso tiene un aspecto incorrecto o extraño, se procesa correctamente en el servidor, lo que significa que no existe ningún problema funcional.

2. **Errores del explorador de archivos**
    - Cuando se trabaja con una instancia de SQL Server 2017 CTP 2.0 basada en Windows, la interfaz de usuario del explorador de archivos puede no abrirse si el servidor tiene instalados una unidad de disquete vacía o un disco fijo protegido por BitLocker. 
    - La interfaz de usuario del explorador de archivos ya no es compatible con las versiones de SQL Server 2017 previas a CTP 2.0.
    


3. **Una sola cuenta de Azure Active Directory puede iniciar sesión para una instancia de SSMS utilizando la autenticación universal de Active Directory.**  
    Esta restricción se limita a la autenticación universal de Active Directory. Puede iniciar sesión en servidores diferentes mediante la autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.
    
    Como alternativa, puede utilizar otra instancia de SSMS para iniciar sesión con otra cuenta de Azure Active Directory. 
    
4. **Los comandos del marco de aplicación de capa de datos (DacFx) y el Diseñador de esquemas en SSMS no admiten la autenticación universal de Active Directory.**  
    Los comandos que utiliza DacFx (por ejemplo, importar y exportar) y el Diseñador de esquemas en SSMS no admiten actualmente la autenticación universal de Active Directory.
    
    Como solución alternativa, puede usar las otras formas de autenticación proporcionada en SSMS - autenticación de contraseña de Active Directory, la autenticación integrada de Active Directory o la autenticación de SQL Server.

5. **SSMS 17.x solo puede conectarse a instancias de SQL Server 2017 Integrated Services (SSIS 2017).**  
    Hay una limitación de compatibilidad conocida con SQL Server Integration Services que impide la conexión a versiones anteriores.
    
    Como solución alternativa para este problema, puede conectarse a la instancia de SQL Server Integration Service mediante la [versión SSMS alineado con la instancia SSIS.](../ssms/previous-sql-server-management-studio-releases.md) 
  
5. **SSMS no guardará los planes de mantenimiento de SQL Server 2008 R2 y versiones anteriores de SQL Server.**  
    Se trata de una limitación conocida que esperamos solucionar en el futuro. Mientras tanto, puede usar la [versión de SSMS de 2014](../ssms/previous-sql-server-management-studio-releases.md) para guardar los planes de mantenimiento.  
    
5. **Las instalaciones de SSMS que no estén en inglés pueden requerir la instalación de un paquete de seguridad adicional.**  
Las versiones localizadas de SSMS en idiomas diferentes al inglés requieren el [paquete de actualización de seguridad KB 2862966](https://support.microsoft.com/en-us/kb/2862966) si se instalan en Windows 8, Windows 7, Windows Server 2012 y Windows Server 2008 R2.

5. **Hacer clic en Ayuda o pulsar F1 no abre la ayuda**  
Algunos entornos muestran lo siguiente al hacer clic en Ayuda o pulsar F1: **Necesitará una aplicación nueva para abrir ms-xhelp**. Este error es un problema conocido y se corregirá en una próxima versión.
  
## <a name="feedback"></a>Comentarios  
  
![needhelp_person_icon](../ssms/media/needhelp_person_icon.png) [Foro de Herramientas de cliente de SQL](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sqltools) |  [Registre un problema o una sugerencia en Microsoft Connect](https://connect.microsoft.com/SQLServer/Feedback).  
  
## <a name="see-also"></a>Vea también  
[Tutorial de SQL Server Management Studio](../ssms/use-sql-server-management-studio.md)  
[Descargar SQL Server Management Studio &#40;SSMS&#41;](../ssms/download-sql-server-management-studio-ssms.md)  
[Versiones anteriores de SQL Server Management Studio](../ssms/previous-sql-server-management-studio-releases.md)  

  

