---
title: Trabajar con el proveedor WMI para la administración de configuración | Microsoft Docs
ms.custom: ''
ms.date: 04/12/2019
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- permissions [WMI]
- connection strings [WMI]
- security [WMI]
- WMI Provider for Configuration Management, connection strings
- WMI Provider for Configuration Management, security
- late binding [WMI]
- WMI Provider for Configuration Management, late binding
- binding [WMI]
ms.assetid: 34daa922-7074-41d0-9077-042bb18c222a
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5e6736c73f7cda435d91e3ec9c9f523bdc08f1b3
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139268"
---
# <a name="working-with-the-wmi-provider-for-configuration-management"></a>Trabajar con el proveedor WMI para la administración de configuración

[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Este artículo proporciona orientación sobre cómo programar con el proveedor WMI para la administración de equipos.

## <a name="binding"></a>Enlace  
 El proveedor WMI para la administración de configuración es un modelo de objetos COM y admite el enlace en tiempo de diseño y en tiempo de ejecución. Con el enlace en tiempo de ejecución puede utilizar lenguajes de script, como VBScript, para manipular mediante programación los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la configuración de red y los alias.  
  
## <a name="specifying-a-connection-string"></a>Especificar una cadena de conexión

Las aplicaciones dirigen el proveedor WMI para la administración de configuración a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la conexión a un espacio de nombres WMI definido por el proveedor. El servicio WMI de Windows asigna este espacio de nombres a la DLL del proveedor y carga el archivo DLL en la memoria. Todas las instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se representan con un único espacio de nombres WMI.

El espacio de nombres predeterminado es el formato siguiente. En el formato, `VV` es el número de versión principal de SQL Server. El número es reconocible ejecutando `SELECT @@VERSION;`.

```console
\\.\root\Microsoft\SqlServer\ComputerManagementVV
```

Cuando se conecta mediante el uso de PowerShell, el líder `\\.\` deben quitarse. Por ejemplo, el código PowerShell siguiente enumera todas las clases WMI de SQL Server 2016, que es la versión principal 13.

```powershell
Get-WmiObject -Namespace 'root\Microsoft\SqlServer\ComputerManagement13' -List
```

<!--
Updated this on 2019-04-12, per:
   ~ https://github.com/MicrosoftDocs/sql-docs/issues/1817
   ~ https://github.com/rrg92/sql-docs/commit/3d518bfc0d55f819c762abc3e5c5c9eed85abe94?diff=unified

Thus from here I (GeneMi = MightyPen) removed the following text about 'instance_name':

'root\Microsoft\SqlServer\ComputerManagement13\instance_name'

where `instance_name` defaults to `MSSQLSERVER` in a default installation of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].
-->

Puede usar código PowerShell siguiente para consultar todos los espacios de nombres WMI ComputerManagement disponibles.

```powershell
gwmi -ns 'root\Microsoft\SqlServer' __NAMESPACE | ? {$_.name -match 'ComputerManagement' } | select name
```

 **Nota:** Si se conecta a través de Firewall de Windows deberá asegurarse de que los equipos están configurados correctamente. Consulte el artículo "Connecting Through Windows Firewall" en la documentación de Instrumental de administración de Windows en [!INCLUDE[msCoName](../../includes/msconame-md.md)] MSDN [sitio Web](https://go.microsoft.com/fwlink/?linkid=15426).  
  
## <a name="permissions-and-server-authentication"></a>Permisos y autenticación del servidor  
 Para tener acceso al proveedor WMI para la administración de configuración, el script de administración de WMI de cliente se debe ejecutar en el contexto de un administrador en el equipo de destino. Necesita ser miembro del grupo administradores de Windows local en el equipo que desea administrar.  
  
 El administrador puede establecer directivas de grupo para controlar el acceso de usuario a los proveedores WMI. Para obtener más información sobre cómo establecer directivas de grupo, vea el tema sobre directiva de grupo y MMC en la Ayuda del Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El script de administración de WMI se puede utilizar para actualizar la cuenta con la que se ejecutan los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 El proveedor WMI para la administración de configuración admite los certificados de seguridad. Para obtener más información acerca de los certificados, consulte [jerarquía de cifrado](../../relational-databases/security/encryption/encryption-hierarchy.md).  
  
## <a name="see-also"></a>Vea también  
 [Administrador de configuración de SQL Server](../../relational-databases/sql-server-configuration-manager.md)  
  
  
