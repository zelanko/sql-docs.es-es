---
title: Crear un ensamblado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- creating assemblies
- UNSAFE assemblies
- CREATE ASSEMBLY statement
- SAFE assemblies
- EXTERNAL_ACCESS assemblies
- assemblies [CLR integration], creating
ms.assetid: a2bc503d-b6b2-4963-8beb-c11c323f18e0
author: rothja
ms.author: jroth
ms.openlocfilehash: 995c3a621e6de5d1b878f28c7c0fffaae3311bd2
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953889"
---
# <a name="creating-an-assembly"></a>Crear un ensamblado
  Los objetos de base de datos administrados, como procedimientos almacenados o desencadenadores, se compilan y, a continuación, se implementan en unidades denominadas ensamblados. Los ensamblados de archivos DLL administrados deben registrarse en [!INCLUDE[msCoName](../../../includes/ssnoversion-md.md)] para poder usar la funcionalidad que proporciona el ensamblado. Para registrar un ensamblado en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , use la instrucción CREATE ASSEMBLY. En este tema se explica cómo registrar un ensamblado en una base de datos mediante la instrucción CREATE ASSEMBLY y cómo especificar la configuración de seguridad del ensamblado.  
  
## <a name="the-create-assembly-statement"></a>La instrucción CREATE ASSEMBLY  
 La instrucción CREATE ASSEMBLY se usa para crear un ensamblado en una base de datos. Este es un ejemplo:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 La cláusula FROM especifica el nombre de ruta de acceso del ensamblado que va a crearse. Esta ruta de acceso puede ser una ruta de acceso UNC (Convención de nomenclatura universal) o una ruta de acceso al archivo físico local en el equipo.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no permite registrar distintas versiones de un ensamblado con el mismo nombre, referencia cultural y clave pública.  
  
 Es posible crear ensamblados que hagan referencia a otros ensamblados. Cuando se crea un ensamblado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , también crea los ensamblados a los que hace referencia el ensamblado de nivel raíz, si los ensamblados a los que se hace referencia aún no se han creado en la base de datos.  
  
 Se conceden permisos a los usuarios de base de datos o a los roles de usuario para crear y, por tanto, establecerse como propietarios de los ensamblados de una base de datos. Para crear ensamblados, el rol o el usuario de base de datos debe disponer del permiso CREATE ASSEMBLY.  
  
 Un ensamblado solo puede hacer referencia correctamente a otros ensamblados si:  
  
-   El ensamblado al que se llama o se hace referencia es propiedad del mismo usuario o del mismo rol.  
  
-   El ensamblado al que se llama o se hace referencia se creó en la misma base de datos.  
  
## <a name="specifying-security-when-creating-assemblies"></a>Especificar la seguridad al crear ensamblados  
 Al crear un ensamblado en una base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], puede especificar uno de los tres niveles distintos de seguridad en los que puede ejecutarse el código: `SAFE`, `EXTERNAL_ACCESS` o `UNSAFE`. Cuando se ejecuta la instrucción `CREATE ASSEMBLY`, se realizan determinadas comprobaciones en el ensamblado de código que pueden provocar que el ensamblado no se registre en el servidor. Para obtener más información, vea el ejemplo de suplantación en [CodePlex](https://msftengprodsamples.codeplex.com/).  
  
 `SAFE` es el conjunto de permisos predeterminado y funciona en la mayoría de los escenarios. Para especificar un nivel de seguridad determinado, debe modificar la sintaxis de la instrucción CREATE ASSEMBLY tal y como se indica a continuación:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = SAFE;  
```  
  
 También es posible crear un ensamblado con el conjunto de permisos `SAFE` simplemente omitiendo la tercera línea del código anterior:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll';  
```  
  
 Cuando el código de un ensamblado se ejecuta con el conjunto de permisos `SAFE`, solo puede realizar tareas de cálculo y acceso a datos en el servidor a través del proveedor administrado en proceso.  
  
### <a name="creating-external_access-and-unsafe-assemblies"></a>Crear ensamblados EXTERNAL_ACCESS y UNSAFE  
 `EXTERNAL_ACCESS` se usa en escenarios en los que el código necesita tener acceso a recursos fuera del servidor, como archivos, la red, el Registro y variables de entorno. Cuando el servidor obtiene acceso a un recurso externo, suplanta el contexto de seguridad del usuario que llama al código administrado.  
  
 El permiso de código `UNSAFE` se usa en escenarios en los que no puede comprobarse la seguridad de un ensamblado o el ensamblado requiere acceso adicional a recursos restringidos, como la API Win32 de [!INCLUDE[msCoName](../../../includes/msconame-md.md)].  
  
 Para crear un ensamblado `EXTERNAL_ACCESS` o `UNSAFE` en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], debe cumplirse una de las dos condiciones siguientes:  
  
1.  El ensamblado está firmado con un nombre seguro o firmado mediante Authenticode con un certificado. Este nombre seguro (o certificado) se crea dentro de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como una clave asimétrica (o certificado) y dispone de un inicio de sesión correspondiente con permiso `EXTERNAL ACCESS ASSEMBLY` (para ensamblados de acceso externo) o permiso `UNSAFE ASSEMBLY` (para ensamblados no seguros).  
  
2.  El propietario de la base de datos (DBO) tiene `EXTERNAL ACCESS ASSEMBLY` `EXTERNAL ACCESS` el permiso (para ensamblados) o `UNSAFE ASSEMBLY` (para `UNSAFE` ensamblados), y la base de datos tiene la [propiedad de base de datos TRUSTWORTHY](../../security/trustworthy-database-property.md) establecida en `ON` .  
  
 Las dos condiciones indicadas anteriormente también se comprueban en el momento de carga del ensamblado (que incluye la ejecución). Para cargar el ensamblado debe cumplirse al menos una de las condiciones.  
  
 Se recomienda que la [propiedad de base de datos TRUSTWORTHY](../../security/trustworthy-database-property.md) de una base de datos no se establezca en `ON` solo para ejecutar el código de Common Language Runtime (CLR) en el proceso de servidor. En lugar de ello, es aconsejable crear una clave asimétrica a partir del archivo de ensamblado de la base de datos maestra. A continuación debe crearse un inicio de sesión asignado a esta clave asimétrica y debe concederse el permiso `EXTERNAL ACCESS ASSEMBLY` o `UNSAFE ASSEMBLY` al inicio de sesión.  
  
 Las [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones siguientes antes de ejecutar la instrucción CREATE Assembly.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll'     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey     
GRANT EXTERNAL ACCESS ASSEMBLY TO SQLCLRTestLogin;   
GO   
```  
  
> [!NOTE]  
>  Debe crear un nuevo inicio de sesión para asociarlo a la clave asimétrica. Este inicio de sesión solamente se usa para conceder permisos; no tiene que asociarse a ningún usuario ni usarse dentro de la aplicación.  
  
 Para crear un ensamblado `EXTERNAL ACCESS`, el creador debe contar con permiso `EXTERNAL ACCESS`. Este permiso se especifica al crear el ensamblado:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = EXTERNAL_ACCESS;  
```  
  
 Las [!INCLUDE[tsql](../../../includes/tsql-md.md)] instrucciones siguientes antes de ejecutar la instrucción CREATE Assembly.  
  
```  
USE master;   
GO    
  
CREATE ASYMMETRIC KEY SQLCLRTestKey FROM EXECUTABLE FILE = 'C:\MyDBApp\SQLCLRTest.dll';     
CREATE LOGIN SQLCLRTestLogin FROM ASYMMETRIC KEY SQLCLRTestKey ;    
GRANT UNSAFE ASSEMBLY TO SQLCLRTestLogin ;  
GO  
```  
  
 Para especificar que un ensamblado se cargue con el permiso `UNSAFE`, debe especificar el conjunto de permisos `UNSAFE` al cargar el ensamblado en el servidor:  
  
```  
CREATE ASSEMBLY SQLCLRTest  
FROM 'C:\MyDBApp\SQLCLRTest.dll'  
WITH PERMISSION_SET = UNSAFE;  
```  
  
 Para obtener más información sobre los permisos de cada configuración, vea [CLR Integration Security](../security/clr-integration-security.md).  
  
## <a name="see-also"></a>Consulte también  
 [Administrar ensamblados de integración CLR](managing-clr-integration-assemblies.md)   
 [Modificar un ensamblado](altering-an-assembly.md)   
 [Quitar un ensamblado](dropping-an-assembly.md)   
 [Seguridad de acceso del código de integración CLR](../security/clr-integration-code-access-security.md)   
 [Propiedad de base de datos TRUSTWORTHY](../../security/trustworthy-database-property.md)   
 [Permitir llamadores de confianza parcial](../../../database-engine/dev-guide/allowing-partially-trusted-callers.md)  
  
