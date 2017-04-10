---
title: "Consideraciones de seguridad para un runtime de R en SQL Server | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "04/01/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d5065197-69e6-4fce-9654-00acaecc148b
caps.latest.revision: 15
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# Consideraciones de seguridad para un runtime de R en SQL Server
  Este tema proporciona un información general de las consideraciones de seguridad para trabajar con [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para obtener más información sobre cómo administrar el servicio y aprovisionar las cuentas de usuario usadas para ejecutar scripts de R, consulte [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Uso del firewall para restringir el acceso de red mediante R  
 En el método de instalación sugerido, se utiliza una regla del Firewall de Windows para bloquear todo el acceso de red saliente de los procesos del runtime de R. Se deben crear reglas de Firewall para impedir al proceso de runtime de R descargar paquetes o realizar otras llamadas de red que podrían ser malintencionadas.  
  
 Se recomienda encarecidamente que active el Firewall de Windows (u otro firewall de su elección) para bloquear el acceso de red mediante el runtime de R.  
  
 Si usa otro programa de firewall, también puede crear reglas para bloquear la conexión de red saliente para el runtime de R estableciendo reglas para las cuentas de usuario locales o para el grupo representado por el grupo de cuentas de usuario.   
Para obtener más información, consulte [Configure and Manage Advanced Analytics Extensions](../../advanced-analytics/r-services/configure-and-manage-advanced-analytics-extensions.md).  
  
## Métodos de autenticación admitidos para contextos de proceso remoto 
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] Ahora es compatible con los inicios de sesión de autenticación integrada de Windows y SQL al crear conexiones entre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y un cliente de ciencia de datos remotos. 
  
 Por ejemplo, si está desarrollando una solución de R en el equipo portátil y desea realizar cálculos en el equipo de SQL Server, debe crear un origen de datos de SQL Server en R, usando la **rx** funciones y la definición de una cadena de conexión en función de sus credenciales de Windows. Al cambiar la _calcular contexto_ desde su equipo portátil en el equipo de SQL Server, si la cuenta de Windows tiene los permisos necesarios, todo el código R se ejecutará en el equipo de SQL Server. Además, cualquier consultas SQL que se ejecuta como parte del código R se ejecutará bajo también sus credenciales. 
 
 Aunque también se puede usar un inicio de sesión SQL en la cadena de conexión para un origen de datos de SQL Server, el uso de un inicio de sesión requiere que la instancia de SQL Server permiten la autenticación de modo mixto.
 
 ### Autenticación implícita
  
 En general el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] el tiempo de ejecución de R se inicia y ejecuta scripts de R en su propia cuenta. Sin embargo, si el script de R realiza una llamada ODBC, el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] suplanta las credenciales del usuario que envió el comando para asegurarse de que no la llamada ODBC. Esto se denomina *autenticación implícita*. 
 
 > [!IMPORTANT] 
 >
 > Para la autenticación implícita correcta, el grupo de usuarios de Windows que contiene las cuentas de trabajo (de forma predeterminada, **SQLRUser**) debe tener una cuenta en la base de datos maestra para la instancia y esta cuenta deben asignarse permisos para conectarse a la instancia.  
  
## No se admite para el cifrado en reposo  
 El cifrado de datos transparente no se admite para los datos enviados o recibidos desde el runtime de R. Por este motivo, el cifrado en reposo **no** se aplicará a ningún dato que se utilice en scripts de R, en ningún dato guardado en disco o en ningún resultado intermedio persistente.  
 
 ## Vea también
 [Escriba la descripción del vínculo](../../advanced-analytics/r-services/configuration-sql-server-r-services.md) 
  