---
title: "Instalaci&#243;n de servicios de SQL Server R en una m&#225;quina Virtual de Azure | Microsoft Docs"
ms.custom: ""
ms.date: "12/07/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c3c223b8-75c4-412e-a319-d57ecf6533af
caps.latest.revision: 11
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 8
---
# Instalaci&#243;n de servicios de SQL Server R en una m&#225;quina Virtual de Azure
 
Si implementa una máquina virtual de Azure que incluye [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], ahora puede seleccionar servicios de R como una característica que se agregará a la instancia cuando se crea la máquina Virtual. 



+ [Crear una nueva máquina Virtual con SQL Server 2016 y R Services](#new)
+ [Agregar R Services a una máquina virtual existente con SQL Server 2016](#existing)

## <a name="a-namenewacreate-a-new-sql-server-2016-enterprise-virtual-machine-with-r-services-enabled"></a><a name="new"></a>Crear una nueva máquina de Virtual de SQL Server 2016 Enterprise con R Services habilitado

1. En el Portal de Azure, haga clic en MÁQUINAS VIRTUALES y, a continuación, haga clic en NUEVO.
2. Seleccione SQL Server 2016 Enterprise Edition.
3. Configurar los permisos de nombre y la cuenta de servidor y seleccione un plan de precios.
4. En el paso 4 de la máquina Virtual de Asistente para, la instalación en **configuración de SQL Server**, busque **R Services (Advanced Analytics)** y haga clic en **Habilitar**.
5. Revise el resumen presentado para la validación y haga clic en **Aceptar**.
6. Cuando la máquina virtual está lista, conectarse a él y abra SQL Server Management Studio, que viene preinstalado. R Services está listo para ejecutarse. 
7. Para comprobarlo, puede abrir una nueva ventana de consulta y ejecutar una instrucción sencilla como siguientes, que usa R para generar una secuencia de números del 1 al 10.
   ```
    execute sp_execute_external_script
    @language = N'R'
    , @script = N' OutputDataSet <- as.data.frame(seq(1, 10, ));'
    , @input_data_1 = N'   ;'
    WITH RESULT SETS (([Sequence] int NOT NULL));
   ```
6. Si va a conectar a la instancia de un cliente de ciencia de datos remotos, completar [pasos adicionales](#additional-steps) según sea necesario.


## <a name="additional-steps"></a>Pasos adicionales  

Algunos pasos adicionales podrían ser necesario usar R Services si espera que los clientes remotos obtener acceso al servidor como contexto de ejecución de un servidor SQL remoto.

### <a name="a-namefirewallaunblock-the-firewall"></a><a name="firewall"></a>Desbloquee el firewall  
  
Debe cambiar una regla de firewall en la máquina virtual para asegurarse de que puede tener acceso a la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia desde un cliente de ciencia de datos remotos.  En caso contrario, es posible que no pueda utilizar compute contextos que requieren el uso de área de trabajo de la máquina virtual. 

De forma predeterminada, el firewall en la máquina virtual de Azure incluye una regla que bloquea la red acceso para las cuentas de usuario locales de R.  
  
Para habilitar el acceso a los servicios de R desde los clientes de ciencia de datos remotos:
1. En la máquina virtual, abra Firewall de Windows con seguridad avanzada.
2. Seleccione **reglas de salida**
3. Deshabilite la regla siguiente:  
  
     `Block network access for R local user accounts in SQL Server instance MSSQLSERVER`  
  
### <a name="enable-odbc-callbacks-for-remote-clients"></a>Habilitar las devoluciones de llamada ODBC para los clientes remotos

Si espera que los clientes de R que llamen al servidor que necesitará emitir consultas de ODBC como parte de sus soluciones de R, debe asegurarse de que el Launchpad puede realizar llamadas ODBC en nombre del cliente remoto. Para ello, debe permitir que las cuentas de trabajo SQL que se Launchpad sirven para iniciar sesión en la instancia.
Para obtener más información, vea [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 

### <a name="a-namenetworkaadd-network-protocols"></a><a name="network"></a>Agregar protocolos de red  
  
+ Habilitar canalizaciones con nombre
  
  [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] usa el protocolo de canalizaciones con nombre para las conexiones entre los equipos cliente y servidor y para algunas conexiones internas. Si canalizaciones con nombre no está habilitada, debe instalar y habilitar en ambas máquina virtual de Azure y en los clientes de ciencia de datos que se conectan al servidor.  
  
+ Habilite TCP/IP

  TCP/IP es necesaria para las conexiones de bucle invertido para SQL Server R Services. Si recibe el siguiente error, habilite TCP/IP en la máquina virtual que es compatible con la instancia DBNETLIB; SQL Server no existe o se denegó el acceso.

## <a name="how-to-disable-r-services-on-an-instance"></a>Cómo deshabilitar R Services en una instancia

También puede habilitar o deshabilitar la característica en una máquina virtual existente en cualquier momento. 

1. Abra la hoja de la máquina virtual
2. Haga clic en **configuración**, y seleccione **configuración de SQL Server**.


## <a name="a-nameexistingaadd-sql-server-r-services-to-an-existing-sql-server-2016-enterprise-virtual-machine"></a><a name="existing"></a>Agregar SQL Server R Services a una máquina virtual existente de SQL Server 2016 Enterprise

Si ha creado una máquina Virtual de Azure con SQL Server 2016 que no incluía R Services, puede agregar la característica siguiendo estos pasos:

1. Vuelva a ejecutar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el programa de instalación y agregue la característica en el **Configuración del servidor** página del asistente.
2. Habilitar la ejecución de scripts externos y reiniciar el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instancia. Para obtener más información, consulte vea [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md).
3. (Opcional) Configurar el acceso de la base de datos para las cuentas de trabajo de R, si es necesario para la ejecución de scripts remotos.
   Para obtener más información, vea [Set Up SQL Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md). 
3. (Opcional) Modificar una regla de firewall en la máquina virtual de Azure, si va a permitir la ejecución del script de R desde los clientes de ciencia de datos remotos. Para obtener más información, vea [desbloquee el firewall](#firewall).
4. Instala ni habilita las bibliotecas de red necesarios. Para obtener más información, vea [Agregar protocolos de red](#network).

## <a name="see-also"></a>Vea también
[Configurar Sql Server R Services](../../advanced-analytics/r-services/set-up-sql-server-r-services-in-database.md)