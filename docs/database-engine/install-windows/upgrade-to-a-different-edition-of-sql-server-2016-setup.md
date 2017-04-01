---
title: "Actualizar a una edici&#243;n diferente de SQL Server 2016 (programa de instalaci&#243;n) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 31d16820-d126-4c57-82cc-27701e4091bc
caps.latest.revision: 27
ms.author: "mikeray"
manager: "jhubbard"
---
# Actualizar a una edici&#243;n diferente de SQL Server 2016 (programa de instalaci&#243;n)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] admite la actualización de edición entre las diferentes ediciones de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener información sobre rutas de actualización de ediciones admitidas, vea [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md). Antes de que se inicie la actualización de edición de una instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], consulte los temas siguientes:  
  
-   [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md)  
  
-   [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md)  
  
-   [Límites de la capacidad de cálculo de cada edición de SQL Server](../../sql-server/compute-capacity-limits-by-edition-of-sql-server.md)  
  
-   [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)  
  
> [!NOTE]  
>  **[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno en clúster:** basta con actualizar la edición en uno de los nodos del clúster de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Este nodo puede ser activo o pasivo, y el motor no pone los recursos sin conexión durante la actualización de la edición. Después de actualizar la edición, es necesario reiniciar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o conmutar por error a otro nodo diferente.  
  
## Requisitos previos  
 En instalaciones locales, debe ejecutar el programa de instalación como administrador. Si instala [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde un recurso compartido remoto, deberá usar una cuenta de dominio que tenga permisos de lectura para dicho recurso.  
  
> [!IMPORTANT]  
>  Para activar el cambio de edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe reiniciar los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esto tendrá como consecuencia un tiempo de inactividad mientras los servicios están sin conexión.  
  
## Procedimiento  
  
#### Para actualizar a una edición diferente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
1.  Inserte el medio de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En la carpeta raíz, haga doble clic en setup.exe o inicie el Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde Herramientas de configuración. Para realizar la instalación desde un recurso compartido de red, localice la carpeta raíz de dicho recurso y, a continuación, haga doble clic en Setup.exe.  
  
2.  Para actualizar una instancia existente de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] a una edición diferente, en el Centro de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] haga clic en **Mantenimiento**y, a continuación, seleccione **Actualización de edición**.  
  
3.  Si son necesarios los archivos auxiliares del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , el citado programa se encarga de instalarlos. Si se le solicita que reinicie el equipo, hágalo antes de continuar.  
  
4.  El Comprobador de configuración del sistema ejecuta una operación de detección en el equipo. Para continuar, haga clic en **Aceptar**.  
  
5.  En la página Clave del producto, haga clic en un botón de opción para indicar si está actualizando a una edición gratuita de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o si tiene una clave de PID para una versión de producción del producto. Para obtener más información, vea [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) y [Actualizaciones de ediciones y versiones admitidas](../../database-engine/install-windows/supported-version-and-edition-upgrades.md).  
  
6.  En la página Términos de licencia, lea el contrato de licencia y active la casilla para aceptar los términos y condiciones de la licencia. Para continuar, haga clic en **Siguiente**. Para salir del programa de instalación, haga clic en **Cancelar**.  
  
7.  En la página Seleccionar instancia, especifique la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que va a actualizar.  
  
8.  La página Reglas de actualización de edición valida la configuración del equipo antes de que empiece la operación de actualización de la edición.  
  
9. La página Listo para actualizar la edición muestra una vista de árbol de las opciones de instalación que se especificaron durante la instalación. Para continuar, haga clic en **Actualizar**.  
  
10. Durante el proceso de actualización de la edición, se han de reiniciar los servicios para que se reconozca la nueva configuración. Una vez actualizada la edición, la página de operación completada proporciona un vínculo al archivo de registro de resumen para la actualización de la edición. Para cerrar el asistente, haga clic en **Cerrar**.  
  
11. La página Completada proporciona un vínculo al archivo de registro de resumen para la instalación y otras notas importantes.  
  
12. Si el programa indica que se reinicie el equipo, hágalo ahora. Es importante leer el mensaje del Asistente para la instalación tras completar el programa de instalación. Para obtener más información sobre los archivos de registro de instalación, vea [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
13. Si ha realizado la actualización desde [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], deberá llevar a cabo pasos adicionales antes usar la instancia actualizada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
    -   Habilite el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en Windows SCM.  
  
    -   Aprovisione la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Además de los pasos anteriores, puede que tenga que realizar lo siguiente si ha efectuado la actualización a partir de [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)]:  
  
-   Los usuarios que estaban aprovisionados en [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] siguen estándolo después de la actualización. En concreto, el grupo BUILTIN\Users sigue estando aprovisionado. Deshabilite, quite o vuelva a aprovisionar estas cuentas según sea necesario. Para obtener más información, vea [Configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
-   Los tamaños y el modo de recuperación de las bases de datos del sistema tempdb y model permanecen inalterados después de la actualización. Vuelva a configurar estos valores según sea necesario. Para obtener más información, vea [Realizar copias de seguridad y restaurar bases de datos del sistema &#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-and-restore-of-system-databases-sql-server.md).  
  
-   Las bases de datos de plantilla permanecen en el equipo después de la actualización.  
  
## Vea también  
 [Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)   
 [Compatibilidad con versiones anteriores](../Topic/Backward%20Compatibility_deleted.md)  
  
  