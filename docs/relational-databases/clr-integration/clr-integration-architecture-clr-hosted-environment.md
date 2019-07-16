---
title: Entorno de CLR hospedado | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- type-safe code [CLR integration]
- UNSAFE permission set
- run-time environments [CLR integration]
- common language runtime [SQL Server], about CLR integration
- application domains [CLR integration]
- host protection attributes [CLR integration]
- managed code [SQL Server], common language runtime
- permission sets [CLR integration]
- reliability [CLR integration]
- SAFE permission set
- code access security [CLR integration]
- EXTERNAL_ACCESS permission set
- verifying type safety
- scalability [CLR integration]
- hosted environments [CLR integration]
- HPAs [CLR integration]
ms.assetid: d280d359-08f0-47b5-a07e-67dd2a58ad73
author: rothja
ms.author: jroth
ms.openlocfilehash: cdef6129f6cdc513382a747e82d84dd27fc433eb
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68068479"
---
# <a name="clr-integration-architecture---clr-hosted-environment"></a>Arquitectura de integración CLR: entorno hospedado CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  La integración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con .NET Framework Common Language Runtime (CLR) permite a los programadores de base de datos usar lenguajes como Visual C#, Visual Basic .NET y Visual C++. Las funciones, procedimientos almacenados, desencadenadores, tipos de datos y agregados pertenecen a los tipos de lógica de negocios que los programadores pueden escribir con estos lenguajes.  
  
  CLR presenta memoria de recopilación de elementos no utilizados, subprocesamiento preferente, servicios de metadatos (reflexión de tipos), capacidad de comprobar el código y seguridad de acceso del código. CLR usa metadatos para localizar y cargar clases, colocar instancias en memoria, resolver invocaciones a métodos, generar código nativo, exigir mecanismos de seguridad y establecer los límites del contexto en tiempo de ejecución.  
  
 CLR y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], como entornos de tiempo de ejecución, se diferencian en el modo en que administran la memoria, los subprocesos y la sincronización. En este tema se describe el modo en que estos dos tiempos de ejecución se integran para que todos los recursos del sistema se administren uniformemente. En este tema también se describe el modo en que la seguridad de acceso del código (CAS) de CLR y la seguridad de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se integran para proporcionar un entorno de ejecución confiable y seguro para el código de usuario.  
  
## <a name="basic-concepts-of-clr-architecture"></a>Conceptos básicos de la arquitectura CLR  
 En .NET Framework, un programador escribe un lenguaje de alto nivel que implementa una clase que define su estructura (por ejemplo, los campos o las propiedades de la clase) y sus métodos. Algunos de estos métodos pueden ser funciones estáticas. La compilación del programa genera un archivo denominado ensamblado que contiene el código compilado en el lenguaje intermedio de [!INCLUDE[msCoName](../../includes/msconame-md.md)] (MSIL) y un manifiesto que contiene todas las referencias a ensamblados dependientes.  
  
> [!NOTE]  
>  Los ensamblados constituyen un elemento vital para la arquitectura CLR; son las unidades de empaquetado, implementación y control de versiones del código de aplicación de .NET Framework. El uso de ensamblados permite implementar el código de aplicación dentro de la base de datos y proporciona un modo uniforme de administrar, realizar copias de seguridad y restaurar aplicaciones de base de datos completas.  
  
 El manifiesto de ensamblado contiene metadatos sobre el ensamblado, que describen todas las estructuras, campos, propiedades, clases, relaciones de herencia, funciones y métodos definidos en el programa. El manifiesto establece la identidad del ensamblado, especifica los archivos que componen la implementación del ensamblado, especifica los tipos y los recursos que forman el ensamblado, desglosa en elementos las dependencias en tiempo de compilación de otros ensamblados y especifica el conjunto de permisos necesarios para que el ensamblado se ejecute correctamente. Esta información se usa en tiempo de compilación para resolver referencias, exigir el cumplimiento de las directivas de enlace de versión y validar la integridad de los ensamblados cargados.  
  
 .NET Framework admite atributos personalizados para anotar clases, propiedades, funciones y métodos con información adicional que la aplicación puede capturar en metadatos. Todos los compiladores de .NET Framework usan estas anotaciones sin interpretarlas y las almacenan como metadatos de ensamblado. Estas anotaciones pueden examinarse del mismo modo que cualquier otro metadato.  
  
 MSIL ejecuta el código administrado en CLR, en lugar ejecutarlo directamente el sistema operativo. Las aplicaciones de código administrado adquieren servicios de CLR, como la recolección automática de elementos no utilizados, la comprobación de tipos en tiempo de ejecución y la compatibilidad con la seguridad. Estos servicios ayudan a proporcionar un comportamiento uniforme independiente de la plataforma y del lenguaje a las aplicaciones de código administrado.  
  
## <a name="design-goals-of-clr-integration"></a>Diseñar objetivos de integración CLR  
 Cuando el código de usuario se ejecuta dentro del entorno CLR hospedado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (que recibe el nombre de integración CLR), se aplican los siguientes objetivos de diseño:  
  
###### <a name="reliability-safety"></a>Confiabilidad (seguridad)  
 El código de usuario no debería tener permiso para llevar a cabo operaciones que pongan en peligro la integridad del proceso del motor de base de datos, como mostrar un cuadro de mensaje que solicite una respuesta por parte del usuario o salir del proceso. El código de usuario no debería poder sobrescribir los búferes de memoria del motor de base de datos o las estructuras de datos internas.  
  
###### <a name="scalability"></a>Escalabilidad  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y CLR tienen distintos modelos internos de programación y administración de memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite un modelo de subprocesos cooperativo, no preferente, en el que los subprocesos se ejecutan de forma voluntaria y periódica o cuando están esperando bloqueos o E/S. CLR admite un modelo de subprocesos preferente. Si el código de usuario que se ejecuta dentro de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede llamar directamente a los tipos primitivos de subprocesamiento del sistema operativo, significa que no se integra bien en el programador de tareas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y que puede degradar la escalabilidad del sistema. CLR no distingue entre la memoria virtual y física, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] administra la memoria física directamente y se le exige que use la memoria física dentro de un límite configurable.  
  
 Los distintos modelos de subprocesamiento, programación y administración de memoria presentan un desafío de integración para un sistema de administración de bases de datos relacionales (RDBMS) que se escala con objeto de admitir miles de sesiones de usuarios simultáneas. La arquitectura debe garantizar que la escalabilidad del sistema no se vea en peligro por el hecho de que el código de usuario llame directamente a las interfaces de programación de aplicaciones (API) para los tipos primitivos de subprocesamiento, memoria y sincronización.  
  
###### <a name="security"></a>Seguridad  
 El código de usuario que se ejecuta en la base de datos debe cumplir las normas de autenticación y autorización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al obtener acceso a objetos de base de datos como tablas y columnas. Además, los administradores de bases de datos deben ser capaces de controlar el acceso a los recursos del sistema operativo, como el acceso a archivos y a la red, desde el código de usuario que se ejecuta en la base de datos. Esto adquiere importancia cuando los lenguajes de programación administrados (a diferencia de los lenguajes no administrados, como Transact-SQL) proporcionan distintas API para obtener acceso a dichos recursos. El sistema debe proporcionar un modo seguro para que el código de usuario obtenga acceso a los recursos del equipo fuera del proceso de [!INCLUDE[ssDE](../../includes/ssde-md.md)]. Para más información, consulte [CLR Integration Security](../../relational-databases/clr-integration/security/clr-integration-security.md).  
  
###### <a name="performance"></a>Rendimiento  
 El código de usuario administrado que se ejecuta en [!INCLUDE[ssDE](../../includes/ssde-md.md)] debe tener un rendimiento de cálculo comparable a ese mismo código ejecutado fuera del servidor. El acceso a la base de datos desde el código de usuario administrado no es tan rápido como el [!INCLUDE[tsql](../../includes/tsql-md.md)] nativo. Para obtener más información, consulte [rendimiento de la integración CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md).  
  
## <a name="clr-services"></a>CLR Services  
 CLR ofrece varios servicios para ayudar a lograr los objetivos de diseño de la integración CLR con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###### <a name="type-safety-verification"></a>Comprobación de la seguridad de tipos  
 El código con seguridad de tipos es código que obtiene acceso a las estructuras de memoria siguiendo métodos perfectamente definidos. Por ejemplo, dada una referencia válida a un objeto, el código con seguridad de tipos puede obtener acceso a la memoria en desplazamientos fijos que se correspondan con miembros de campo reales. Sin embargo, si el código obtiene acceso a la memoria en desplazamientos arbitrarios que se encuentran dentro o fuera del intervalo de memoria perteneciente al objeto, significa que no tiene seguridad de tipos. Cuando los ensamblados se cargan en CLR, antes de que MSIL se compile mediante la compilación Just-In-Time (JIT), el tiempo de ejecución realiza una fase de comprobación que examina el código para determinar su seguridad de tipos. El código que supera correctamente esta comprobación se denomina código con seguridad de tipos comprobable.  
  
###### <a name="application-domains"></a>Dominios de aplicación  
 CLR admite la noción de dominios de aplicación como zonas de ejecución dentro de un proceso de host donde los ensamblados de código administrado pueden cargarse y ejecutarse. El límite del dominio de aplicación proporciona aislamiento entre los ensamblados. Los ensamblados se aíslan en lo que se refiere a la visibilidad de variables estáticas y miembros de datos, y a la capacidad de llamar al código de forma dinámica. Los dominios de aplicación también constituyen el mecanismo de carga y descarga de código. Solo es posible descargar código de la memoria descargando el dominio de aplicación. Para obtener más información, consulte [dominios de aplicación y seguridad de la integración de CLR](https://msdn.microsoft.com/library/54ee904e-e21a-4ee7-b4ad-a6f6f71bd473).  
  
###### <a name="code-access-security-cas"></a>Seguridad de acceso del código (CAS)  
 El sistema de seguridad de CLR proporciona un modo de controlar qué tipos de operaciones puede llevar a cabo el código administrado mediante la asignación de permisos al código. Los permisos de acceso a código se asignan según la identidad del código (por ejemplo, la firma del ensamblado o el origen del código).  
  
 CLR proporciona una directiva de equipos que puede establecer el administrador del equipo. Esta directiva define las concesiones de permisos para cualquier código administrado que se ejecute en el equipo. Además, hay una directiva de seguridad de nivel de host que puedan usar los hosts, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para especificar restricciones adicionales en el código administrado.  
  
 Si una API administrada de .NET Framework expone operaciones en recursos protegidos por un permiso de acceso a código, la API solicitará ese permiso antes de obtener acceso al recurso. Esta solicitud hace que el sistema de seguridad de CLR active una comprobación completa de cada unidad de código (ensamblado) en la pila de llamadas. Solo si la cadena de llamadas completa tiene permiso obtendrá acceso al recurso.  
  
 Tenga en cuenta que la capacidad de generar código administrado de forma dinámica, mediante la API Reflection.Emit, no se admite dentro del entorno CLR hospedado en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Dicho código no tendría los permisos CAS necesarios para ejecutarse y, por lo tanto, generaría un error en tiempo de ejecución. Para obtener más información, consulte [CLR Integration Code Access Security](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
###### <a name="host-protection-attributes-hpas"></a>Atributos de protección del host (HPA)  
 CLR proporciona un mecanismo para anotar API administradas que forman parte de .NET Framework con determinados atributos que pueden ser de interés para un host de CLR. Algunos ejemplos de estos atributos son los siguientes:  
  
-   SharedState, que indica si la API expone la capacidad de crear o administrar un estado compartido (por ejemplo, campos de clase estática).  
  
-   Synchronization, que indica si la API expone la capacidad de llevar a cabo una sincronización entre los subprocesos.  
  
-   ExternalProcessMgmt, que indica si la API expone una forma de controlar el proceso de host.  
  
 Dados estos atributos, el host puede especificar una lista de atributos HPA, como el atributo SharedState, que no deberían permitirse en el entorno hospedado. En este caso, CLR rechaza los intentos del código de usuario de llamar a las API anotadas por los HPA en la lista de atributos prohibidos. Para obtener más información, consulte [atributos de protección de Host y programación de integración de CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
## <a name="how-sql-server-and-the-clr-work-together"></a>Cómo trabajan juntos SQL Server y CLR  
 En esta sección se describe el modo en que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] integra los modelos de subprocesamiento, programación, sincronización y administración de memoria de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y CLR. En concreto, en esta sección se examina la integración a la luz de los objetivos de escalabilidad, confiabilidad y seguridad. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] actúa esencialmente como sistema operativo para CLR cuando se hospeda en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. CLR llama a las rutinas de bajo nivel implementadas por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para el subprocesamiento, la programación, la sincronización y la administración de memoria. Éstos son los mismos tipos primitivos que usa el resto del motor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Este enfoque proporciona varias ventajas de escalabilidad, confiabilidad y seguridad.  
  
###### <a name="scalability-common-threading-scheduling-and-synchronization"></a>Escalabilidad: Común de subprocesamiento, programación y sincronización  
 CLR llama a la API de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a fin de crear subprocesos para ejecutar código de usuario y para su propio uso interno. Para realizar una sincronización entre varios subprocesos, CLR llama a los objetos de sincronización de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esto permite al programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programar otras tareas cuando un subproceso espera en un objeto de sincronización. Por ejemplo, cuando CLR inicia la recolección de elementos no utilizados, todos sus subprocesos esperan a que finalice dicha recopilación de elementos no utilizados. Puesto que el programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conoce los subprocesos CLR y los objetos de sincronización que están esperando, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede programar los subprocesos que están ejecutando otras tareas de base de datos no relacionadas con CLR. Esto también permite a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] detectar interbloqueos que implican bloqueos tomados por los objetos de sincronización CLR y emplear técnicas tradicionales para la eliminación de los interbloqueos.  
  
 El código administrado se ejecuta de forma preferente en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tiene capacidad para detectar y detener subprocesos que no se han producido durante mucho tiempo. La capacidad de enlazar subprocesos CLR con subprocesos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implica que el programador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede identificar subprocesos consecutivos en CLR y administrar su prioridad. Dichos subprocesos consecutivos se suspenden y vuelven a colocarse en la cola. Los subprocesos que se identifican repetidamente como subprocesos consecutivos no tienen permiso para ejecutarse durante un período de tiempo determinado de manera que puedan ejecutarse otros subprocesos de trabajo en ejecución.  
  
> [!NOTE]  
>  El código administrado de ejecución prolongada que obtiene acceso a datos o asigna suficiente memoria para desencadenar la recolección de elementos no utilizados se producirá automáticamente. El código administrado de ejecución prolongada que no obtiene acceso a datos o no asigna suficiente memoria administrada para desencadenar la recolección de elementos no utilizados debe producirse explícitamente llamando a la función System.Thread.Sleep() de .NET Framework.  
  
###### <a name="scalability-common-memory-management"></a>Escalabilidad: Administración de memoria común  
 CLR llama a los tipos primitivos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para asignar y anular la asignación de su memoria. Dado que la memoria usada por CLR se tiene en cuenta a efectos del uso de memoria total del sistema, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede permanecer dentro de sus límites de memoria configurados y asegurarse de que CLR y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no compitan entre sí por obtener más memoria. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] también puede rechazar las solicitudes de memoria de CLR cuando la memoria del sistema está restringida y solicitar a CLR que reduzca su uso de memoria cuando otras tareas necesiten memoria.  
  
###### <a name="reliability-application-domains-and-unrecoverable-exceptions"></a>Confiabilidad: Dominios de aplicación y excepciones irrecuperables  
 Cuando el código administrado de las API de .NET Framework detecta excepciones críticas, como excepciones de memoria insuficiente o desbordamiento de pila, no siempre puede recuperarse de dichos errores y garantizar una semántica coherente y correcta para su implementación. Estas API generan una excepción de anulación de subprocesos en respuesta a estos errores.  
  
 Cuando se hospedan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], dichas anulaciones de subprocesos se controlan de la siguiente forma: CLR detecta cualquier estado compartido en el dominio de aplicación en el que se produce la anulación del subproceso. Para ello, CLR comprueba la presencia de objetos de sincronización. Si hay un estado compartido en el dominio de aplicación, se descarga el propio dominio de aplicación. La descarga del dominio de aplicación detiene las transacciones de base de datos que se estén ejecutando en esos momentos en dicho dominio de aplicación. Dado que la presencia de estado compartido puede aumentar el impacto de dichas excepciones críticas en las sesiones de usuario distintas de la que desencadena la excepción, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y CLR han dado algunos pasos para reducir la probabilidad del estado compartido. Para obtener más información, vea la documentación de .NET Framework.  
  
###### <a name="security-permission-sets"></a>Seguridad: Conjuntos de permisos  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] permite a los usuarios especificar los requisitos de confiabilidad y seguridad para el código implementado en la base de datos. Cuando se cargan los ensamblados en la base de datos, el autor del ensamblado puede especificar uno de los tres conjuntos de permisos para dicho ensamblado: SEGURO, EXTERNAL_ACCESS y UNSAFE.  
  
|||||  
|-|-|-|-|  
|Conjunto de permisos|SAFE|EXTERNAL_ACCESS|UNSAFE|  
|Seguridad de acceso del código|Solo ejecución|Ejecución + acceso a recursos externos|No restringida|  
|Restricciones del modelo de programación|Sí|Sí|Sin restricciones|  
|Requisito de capacidad de comprobación|Sí|Sí|No|  
|Capacidad de llamar a código nativo|Sin|No|Sí|  
  
 SAFE es el modo más confiable y seguro, con restricciones asociadas relativas al modelo de programación permitido. Los ensamblados SAFE tienen permisos suficientes para la ejecución, realización de cálculos y obtención de acceso a la base de datos local. Los ensamblados SAFE deben tener capacidad para comprobar la seguridad de los tipos y no pueden llamar a código no administrado.  
  
 UNSAFE está pensado para el código de alta confianza que solo pueden crear los administradores de bases de datos. Este código de confianza no tiene ninguna restricción de seguridad de acceso del código y puede llamar al código no administrado (nativo).  
  
 EXTERNAL_ACCESS proporciona una opción de seguridad intermedia, que permite al código tener acceso a los recursos externos a la base de datos, pero manteniendo las garantías de confiabilidad de SAFE.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa la capa de directiva CAS de nivel de host para configurar una directiva de host que concede uno de los tres conjuntos de permisos basados en el conjunto de permisos almacenado en los catálogos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El código administrado que se ejecuta dentro de la base de datos siempre obtiene uno de estos conjuntos de permisos de acceso a código.  
  
### <a name="programming-model-restrictions"></a>Restricciones del modelo de programación  
 El modelo de programación para el código administrado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] implica la escritura de funciones, procedimientos y tipos que normalmente no necesitan usar el estado mantenido a lo largo de varias invocaciones o compartir el estado entre varias sesiones de usuario. Además, como se explicó antes, la presencia de estado compartido puede producir excepciones críticas que tienen un impacto en la escalabilidad y la confiabilidad de la aplicación.  
  
 A la vista de estas consideraciones, se desaconseja el uso de variables estáticas y miembros de datos estáticos de las clases que se utilizan en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En el caso de ensamblados SAFE y EXTERNAL_ACCESS, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] examina los metadatos del ensamblado en el momento de creación del ensamblado (CREATE ASSEMBLY) y no puede crear dichos ensamblados si detecta el uso de variables y miembros de datos estáticos.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] También permite las llamadas a API de .NET Framework anotadas con el **SharedState**, **sincronización** y **ExternalProcessMgmt** atributos de protección del host. Esto impide que los ensamblados EXTERNAL_ACCESS y SAFE llamen a cualquiera de las API que habilitan el estado compartido, ejecuten la sincronización y puedan afectar a la integridad del proceso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener más información, consulte [restricciones del modelo de programación de integración de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
## <a name="see-also"></a>Vea también  
 [Seguridad de la integración CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)   
 [Rendimiento de la integración CLR](../../relational-databases/clr-integration/clr-integration-architecture-performance.md)  
  
  
