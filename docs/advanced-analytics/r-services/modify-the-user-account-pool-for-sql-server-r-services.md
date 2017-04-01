---
title: "Modificar el grupo de cuentas de usuario de SQL Server R Services | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58b79170-5731-46b5-af8c-21164d28f3b0
caps.latest.revision: 19
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Modificar el grupo de cuentas de usuario de SQL Server R Services
  Como parte del proceso de instalación de [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], una nueva ventana de *grupo de cuenta de usuario* se crea para admitir la ejecución de tareas mediante el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] service. El propósito de estas cuentas de trabajo es aislar la ejecución simultánea de Scripts de R a diferentes usuarios SQL.
  
  El número de cuentas de usuario de este grupo determina el número de sesiones de R que pueden estar activas simultáneamente.   Si el mismo usuario ejecuta simultáneamente varios scripts de R, todas las sesiones de ejecución para que el usuario usará la misma cuenta de trabajo. En consecuencia, un usuario podría tener 100 scripts R diferentes que se ejecutan al mismo tiempo siempre que se permiten los recursos.

## Configuración predeterminada   
-   En una instancia predeterminada, es el nombre del grupo **SQLRUserGroup**. 
-   En una instancia con nombre, el nombre del grupo predeterminado se utiliza como sufijo con el nombre de instancia: por ejemplo, **SQLRUserGroupMyInstanceName**. 
-   Cuentas: De forma predeterminada, el grupo de la cuenta de usuario contiene 20 cuentas de usuario, denominadas **MSSQLSERVER01** a través de **MSSQLSERVER20** para la instancia predeterminada.  
-   Para una instancia con nombre, las cuentas de usuario se denominan con el nombre de instancia: por ejemplo, **MyInstanceName01** a través de **MyInstanceName20**.  


## Administrar el grupo de usuarios para cada instancia
Crea el grupo de cuentas de Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación para cada instancia en el que está instalado servicios de R, por lo que si ha instalado varias instancias que admiten R, habrá varios grupos de usuarios.
Sin embargo, cada grupo de usuarios está asociado con el [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] de servicio en una instancia específica y no es compatible con trabajos de R que se ejecutan en otras instancias.

De forma predeterminada, el grupo tiene **no** dispone de permisos de inicio de sesión en la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia que está asociado. Si se necesita para habilitar la ejecución de scripts de R por los usuarios, el Administrador de la base de datos debe proporcionar este grupo con **conectarse a** permisos.  

### Cambiar el número de cuentas de trabajo en el grupo de usuarios de Windows

Para modificar el número de usuarios en el grupo de cuenta, debe modificar las propiedades de la [!INCLUDE[rsql_launchpad](../../includes/rsql-launchpad-md.md)] servicio tal y como se describe a continuación.  
  
Las contraseñas asociadas con cada cuenta de usuario se generan aleatoriamente, pero puede cambiarla posteriormente una vez creadas las cuentas.  
  
1. Abra el Administrador de configuración de SQL Server y seleccione **Services de SQL Server**.
2. Haga doble clic en el servicio Launchpad de SQL Server y detener el servicio si se está ejecutando. 
3.  En el **Service** ficha, asegúrese de que el modo de inicio esté establecido en automático. Scripts de R se producirá un error si no se está ejecutando el LaunchPad.
4.  Haga clic en el **avanzadas** ficha y modifique el valor de **recuento de usuarios externos** Si es necesario. Esta configuración controla cuántos usuarios diferentes de SQL puede ejecutar consultas simultáneamente en R. El valor predeterminado es 20 cuentas que en la mayoría de los casos es más que suficiente para admitir las sesiones de R.
5. Opcionalmente, puede establecer la opción **Restablecer la contraseña de los usuarios externos** a _Sí_ Si su organización tiene una directiva que requiere el cambio de contraseña cada 90 días. Esto se regenerarán las contraseñas cifradas que LaunchPad mantiene para las cuentas de usuario.    
6.  Reiniciar el servicio.  

## Permisos adicionales necesarios para la ejecución de secuencias de comandos remotas
Si ejecuta scripts de R con el equipo de SQL Server como remoto calcular contexto, este grupo de trabajo necesita permiso para iniciar sesión en la instancia de SQL Server donde se va a ejecutar scripts de R.

Para obtener más información, consulte [preguntas más frecuentes de instalación y actualización](../../advanced-analytics/r-services/upgrade-and-installation-faq-sql-server-r-services.md). 

  
## Vea también  
 [Configuración (servicios SQL Server R)](../../advanced-analytics/r-services/configuration-sql-server-r-services.md)
  