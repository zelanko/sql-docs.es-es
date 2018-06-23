---
title: Diseñar ensamblados | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 486c6ad507682db3bd7ab06c674164b1d31f34bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36201612"
---
# <a name="designing-assemblies"></a>Diseñar ensamblados
  En este tema se describen los siguientes aspectos que se deben tener en cuenta al diseñar ensamblados:  
  
-   Empaquetar ensamblados  
  
-   Administrar la seguridad del ensamblado  
  
-   Restricciones de los ensamblados  
  
## <a name="packaging-assemblies"></a>Empaquetar ensamblados  
 Un ensamblado puede contener funcionalidad para más de un tipo o una rutina de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en sus clases y métodos. En la mayoría de los casos, resulta conveniente empaquetar la funcionalidad de rutinas que ejecutan funciones relacionadas dentro del mismo ensamblado, especialmente si estas rutinas comparten clases cuyos métodos se llaman unos a otros. Por ejemplo, las clases que efectúan tareas de administración de entradas de datos para desencadenadores de Common Language Runtime (CLR) y procedimientos almacenados de CLR se pueden empaquetar en el mismo ensamblado. Esto se debe a que los métodos correspondientes a estas clases tienen más probabilidad de llamarse unos a otros que los de tareas menos relacionadas.  
  
 Cuando empaquete código en un ensamblado, debe tener en cuenta lo siguiente:  
  
-   Los índices y tipos definidos por el usuario CLR que dependan de funciones definidas por el usuario CLR pueden provocar que haya datos almacenados en la base de datos que dependan del ensamblado. Normalmente, modificar el código de un ensamblado resulta más complejo cuando hay datos almacenados que dependen del ensamblado de la base de datos. Por lo tanto, en general es mejor separar el código en el que se basan las dependencias de datos almacenados (como los tipos y los índices definidos por el usuario que utilizan funciones definidas por el usuario) del código que no tiene tales dependencias de datos almacenados. Para obtener más información, consulte [implementar ensamblados](assemblies-implementing.md) y [ALTER ASSEMBLY &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-assembly-transact-sql).  
  
-   Si parte del código administrado requiere un permiso de mayor nivel, es mejor separar ese código en un ensamblado diferente del correspondiente al código que no requiere ese nivel de permiso.  
  
## <a name="managing-assembly-security"></a>Administrar la seguridad de los ensamblados  
 Es posible controlar el grado de acceso de un ensamblado a los recursos protegidos mediante la seguridad de acceso del código de .NET mientras ejecuta código administrado. Para ello, tiene que especificar uno de estos tres conjuntos de permisos al crear o modificar un ensamblado: SAFE, EXTERNAL_ACCESS o UNSAFE.  
  
### <a name="safe"></a>SAFE  
 SAFE es el conjunto de permisos predeterminado y es el más restrictivo. El código ejecutado por un ensamblado con permisos SAFE no podrá tener acceso a recursos externos del sistema, como los archivos, la red, las variables de entorno o el registro. El código SAFE puede tener acceso a datos de las bases de datos locales de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o puede ejecutar cálculos y lógica de negocios que no impliquen acceso a recursos ajenos a las bases de datos locales.  
  
 La mayoría de ensamblados realizan cálculos y tareas de administración de datos sin necesidad de tener acceso a recursos ajenos a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Por lo tanto, se recomienda SAFE como conjunto de permisos de los ensamblados.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS permite a los ensamblados obtener acceso a ciertos recursos externos del sistema, como los archivos, las redes, los servicios web, las variables de entorno y el registro. Solo los inicios de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con permisos EXTERNAL ACCESS pueden crear ensamblados con EXTERNAL_ACCESS.  
  
 Los ensamblados con SAFE y EXTERNAL_ACCESS pueden incluir código con seguridad de tipos comprobable. Esto significa que dichos ensamblados solo tienen acceso a clases a través de puntos de entrada bien definidos que son válidos para la definición de tipos. Por lo tanto, no pueden tener acceso arbitrariamente a búferes de memoria que no pertenezcan al código. Además, no pueden realizar operaciones que puedan tener un efecto adverso en la estabilidad del proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE proporciona a los ensamblados un acceso sin límites a los recursos situados tanto dentro como fuera de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El código que se ejecuta desde un ensamblado con UNSAFE puede llamar a código no administrado.  
  
 Además, si se especifica UNSAFE, el código incluido en el ensamblado puede realizar operaciones que la comprobación de CLR considera sin seguridad de tipos. Estas operaciones pueden tener acceso a búferes de memoria en el espacio del proceso de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de forma incontrolada. Los ensamblados UNSAFE también pueden trastornar potencialmente el sistema de seguridad de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o de Common Language Runtime. Los permisos UNSAFE solo deben concederlos programadores o administradores experimentados a ensamblados de mucha confianza. Solo los miembros de la **sysadmin** rol fijo de servidor puede crear ensamblados no seguros.  
  
## <a name="restrictions-on-assemblies"></a>Restricciones en los ensamblados  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] impone ciertas restricciones en el código administrado de los ensamblados para asegurarse de que puedan ejecutarse de manera confiable y escalable. Esto significa que, en los ensamblados con SAFE y EXTERNAL_ACCESS, no se permiten ciertas operaciones que pueden comprometer la estabilidad del servidor.  
  
### <a name="disallowed-custom-attributes"></a>Atributos personalizados no permitidos  
 Los ensamblados no se pueden anotar con los siguientes atributos personalizados:  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 Además, los ensamblados con SAFE y EXTERNAL_ACCESS no se pueden anotar con los siguientes atributos personalizados:  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>API de .NET Framework no permitidas  
 Cualquier [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] API que se anota con uno de los **HostProtectionAttributes** no se puede llamar desde ensamblados SAFE y EXTERNAL_ACCESS.  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>Ensamblados de .NET Framework admitidos  
 Cualquier ensamblado al que haga referencia el suyo personalizado se debe cargar en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mediante CREATE ASSEMBLY. Los siguientes ensamblados de [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] ya están cargados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] y, por lo tanto, se les puede hacer referencia mediante ensamblados personalizados sin la necesidad de utilizar CREATE ASSEMBLY.  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>Vea también  
 [Ensamblados &#40;motor de base de datos&#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Seguridad de la integración CLR](security/clr-integration-security.md)  
  
  
